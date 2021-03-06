# Cache databases
<hr>

**Objetivo:** O armazenamento em cache é utilizado para acelerar o processo de leitura de dados ao invés de buscá-lo em sua origem.

## Sumário
1. [O que considerar ao escolher um banco](#o_que_considerar)
1. [Conceitos importantes](#conceitos_importantes)
	- [Técnicas de armazenamento](#tec_armazenamento)
	- [Armazenamento de resultados de queries](#res_queries)
	- [Sincronismo](#sincronismo)
	- [Cache size](#cache_size)
	- [Caching in Server clusters](#server_cluster)
1. [Bancos](#bancos)
1. [Diferenças](#diferencas)
1. [Operações Redis](#operacoes_redis)
1. [Referências](#referencias)

## <a name="o_que_considerar">1. O que considerar ao escolher um banco</a>

- Eviction policies (Políticas de despejo);
- Max size limit
- Persistent store
- Weak references keys
- Statistics

## <a name="conceitos_importantes">2. Conceitos importantes</a>

### <a name="tec_armazenamento">2.1 Técnicas de armazenamento</a>
#### Upfront population
O cache é populado com todos os dados necessários no início da execução.
Esta abordagem requer que todos os dados a serem armazenados já sejam conhecidos.

#####  Vantagens:
Não há tanto delay de leitura de informação, já que todos os dados já estão presentes e não precisam ser buscados externamente.

##### Desvantagens:
O build inicial pode demorar;
Há o risco de dados armazenados nunca serem requisitados.

<hr>

#### Lazy population
O cache é populado apenas quando certo dado é requisitado.
Primeiro verifica-se se o dado já existe no cache. Caso não, deve-se busca-lo em sua origem e inseri-lo.

##### Vantagens:
Dados são armazenados apenas quando requisitados.
Não há delay para o build inicial;

##### Desvantagens:
Não há uma linearidade no delay de leitura, já que na primeira vez o dado sempre será buscado em sua origem.

<hr>

### <a name="res_queries">2.2 Armazenamento de reultados de queries</a>
- Não se deve escolher o armazenamento em cache simplesmente por conta de as queries serem muito lentas. Este na verdade deve ser p último recurso. A otimização deve começar no lado do DB (Verificando a estratégia de fetching e não utilizando queries N+1). Quando esta etapa for finalizada, verifique se todos os índices estão corretos. Estes devem caber na memória RAM, caso contrário a infrá irá começar a aumentar muito.

	- Queries N+1 são nested loops que funcionam como duas queries em execução. A query de fora busca os resultados em uma tabela e a query de dentro busca, para cada linha, o dado correspondente em outra tabela.

- O banco de dados por si só já tem a capacidade de fazer cache dos resultados. Caso o banco seja muito grande e a taxa de criscimento seja alta, deve-se escalar horizontalmente em múltiplos shards.

- Caso estas medidas ainda assim não sejam suficientes, pode-se considerar uma alternativa de cache como o Memcached.

<hr>

### <a name="sincronismo">2.3 Sincronismo</a>
#### Abordagens:
##### Write-through caching
- É um cache que permite leitura e escrita nele.
- Quando um novo dado é inserido no cache, este também é inserido no banco persistente.
- Esta abordagem funciona apenas se o DB persistente possa ser atualizado apenas pelo computador que possui o DB cache. Se todos os dados passam pelo computador com o DB cache, deve-se apenas direciona-los para o DB persistente e atualizar o cache sob demanda.

<hr>

##### Time Based Expiry
- Se o DB persistente pode ser atualizado de outros computadores que não sejam o que possui o DB cache, pode ser um problema manter o sincronismo.
- Uma maneira de manter o sincronismo é definir um tempo para que os dados em cache expirem. E quando este for solicitado novamente, será buscado no DB persistente o dado atualizado e assim persistido no cache.
- Este tempo de expiração deve ser definido de acordo com a necessidade. Mas tenha em mente que menor tempo significa maior quantidade de leitura no DB persistente.

<hr>

##### Active Expiry
- O DB cache é atualizado conforme o DB persistente é atualizado. Quando o sistema com o DB persistente atualiza um dado, também envia uma mensagem para o DB cache expirar o mesmo dado.
- A vantagem desta abordagem é que o dado será atualizado o mais brevemente possível e apenas quando necessário.
- A desvantagem é a necessidade de ter que detectar mudanças no DB persistente. Se dados são inseridos de mais de uma origem, cada uma dessas origens devem reportar que dados foram atualizados. Caso contrário não será possível informar ao computador com cache de que um dado deve ser expirado.

<hr>

#### ACID [ Atomicity, Consistency, Isolation, Durability ]
- As propriedades ACID podem ser comprometidas caso o cache não seja sincronizado corretamente com o DB.
- Deve-se ter cuidado ao atualizar o cache de forma assíncrona, pois isso resulta na perda de consistência (eventual consistency).
	- Eventual consistency é uma abordagem utilizada em sistemas distribuídos para obter alta disponibilidade, e que tem as propriedades BASE (Basically Available, Soft state, Eventual consistency);

<hr>

### <a name="cache_size">2.4 Cache Size</a>
#### Abordagens para controlar o despejo dos dados e liberação de espaço:

##### Time based eviction
- Similar ao Time Based Expiry.
- Esta abordagem pode ser alcançada através de uma thread separada que monitora o cache. Ou a limpeza pode acontecer quando um novo dado for lido ou escrito no cache.

<hr>

##### FIFO
- Quando há a escrita no cache, o registro mais antigo é removido.
- Esta operação de remoção deve entrar em ação apenas quando o max limit do cache for alcançado.

<hr>

##### FILO
- O contrário do FIFO.
- Esta abordagem é útil quando os primeiros valores armazenados são os mais requisitados.

<hr>

##### Least accessed
- Os valores com menor número de acessos são os removidos primeiro.
- Para implementar esta abordagem, deve-se manter um registro de quantas vezes cada valor foi acessado.
- Um ponto para ter atenção nesta abordagem é que os registros mais antigos têm o maior número de acessos. Mesmo que não sejam mais acessados (Caso tenha sido muito acessado no passado). Para evitar esta situação o contador de acesso poderia levar em consideração as últimas X horas. Esta contagem de horas pode complicar ainda mais esta abordagem, então cada situação deve ser estudada.

<hr>

##### Least time between access
- Considera o intervalo de acesso para cada registro.
- Quando um registro é acessado, o cache registra o momento. Quando o registro é acessado novamente, o cache registra o momento e obtém uma média desses intervalos.
- Uma variação desta abordagem é contar o intervalo de acesso apenas para os últimos X acessos. Quando o número de accessos for X, a contagem é resetada para 0 e é feito o registro do momento do último acesso. Isso evita que registros percam 'popularidade' mais rápido do que o número de acessos mínimos tenham sido alcançados.

<hr>

### <a name="server_cluster">2.5 Caching in Server clusters</a>
- Se for usada a abordagem write-through, apenas o server que executa a escrita terá conhecimento sobre o dado.
- São recomendadas as abordagens time based expiration e active expiration para que o sincronismo seja garantido.

## <a name="bancos">3. Bancos</a>

- Memcached
- Redis

## <a name="diferencas">4. Diferenças</a>

- Redis é maior, mais poopular e tem maior suporte do que Memcached.
- O Memcached pode fazer apenas uma parte do que o Redis faz.
- O Memcached ocupa o espaço total definido para seu uso em RAM. Independente de estar sem nenhum registro nele. Enquanto que o Redis irá utilizar apenas o necessário, e a definição de um tamanho máximo é opcional.
- O espaço ocupado por registros em ambos é similar.
- O Redis possui por default a possibilidade de fazer dump dedados por ferramentas de terceiros. O Memcached não oferece essa possibilidade.
- Redis oferece ferramentas para auxiliar na sua escalabilidade ([Redis cluster](https://redis.io/topics/cluster-tutorial) e [Redis sentinel](https://redis.io/topics/sentinel)) enquanto que o Memcached não.
- Redis suporta pub/sup enquanto que o Memcached não;
- Memcached perde os dados quando o server é reiniciado, já que os dados são armazenados em memória apenas. Enquanto que o Redis, por padrão, persiste os dados em disco, mas também oferece a possibilidade de não faze-lo.

## <a name="operacoes_redis">5. Operações Redis</a>

#### Comandos básicos
- `INCR` - Operação atômica para incrementar um valor. Não há problemas de consistência. Incrementa `age` em 1. Caso a chave não exista, é criada;
	- Ex: `INCR age` 
- `EXPIRE` - Expira a chave em X segundos;
	- Ex: `EXPIRE age 10` - expira a chave `age` em 10s;
	- Retorno `-2`: A chave não existe mais;
	- Retorno `-1`: A chave não expira;
- `TTL` - Retorna o `time to live` da chave em segundos;
	- Ex: `TTL age`
	- Quando o valor de uma chave é alterado, o `TTL` dela é resetado para -1, que é o padrão;

#### Listas
- `RPUSH` - Adiciona um valor ao final da lista;
	-Ex: `RPUSH friends 'victor'`
- `LPUSH` - Adiciona um valor no início da lista;
- `LRANGE` - Retorna um subset da lista. O primeiro argumento é o primeiro item e o segundo é o último;
	- Ex:  `LRANGE friends 0 -1` - Rorna todos os itens da lista;
	- `-1` Indica que devem ser retornados elementos até o fim da lista;
- `LLEN` - Retorna o tamanho da lista
- `LPOP` - Remove o primeiro item da lista
- `RPOP` - Remove o último item da lista

#### Sets
- `SAAD` - Adiciona um valor ao set;
	- Ex: `SADD powers 'flight'`
- `SREM` - Remove um valor do set;
	- Ex: `SREM powers 'flight'`
- `SISMEMBER` - Testa se dado valor faz parte do set. `1` caso seja e `0` caso não seja.
	- Ex: `SISMEMBER powers 'flight'`
- `SMEMBERS` - Lista os elementos em um set
- `SUNION` - Une dois sets e retorna um só. Não altera os `sets`.
	- Ex: `SUNION powers subpowers`

#### Sorted sets
Na versão 1.2 do Redis foi adicionado o tipo `sorted set`, onde cada valor tem um score associado a ele. E é este score que será utilizado para ordenar o `set`.
- `ZADD` - Adiciona um valor ao set
	- Ex: `ZADD hackers 1940 'Alan Kay'` `ZADD hackers 1906 'Grace Hopper'` `ZADD hackers 1953 'Richard Stallman'`
- `ZRANGE` - Retorna os valores em ordem crescente;
	- Ex: `ZRANGE hackers 0 -1`

#### [Hashes](https://redis.io/commands#hash)
São mapas de chave-valor. Este é o tipo de dado ideal para representar um objeto
Exemplo:
```
HSET user:1000 name 'Victor Augusto'
HSET user:1000 email 'findme@augustovictor.com.br'
HSET user:1000 password 'pass123'

OU

HMSET user:1000 name 'Victor Augusto' email 'findme@augustovictor.com.br' password 'pass123'
```
- `HGETALL` - Traz todos os dados de um hash;
- `HGET` - Traz o valor de uma propriedade
	- Ex: `HGET user:1000 name`

## <a name="referencias">6. Referências</a>

- https://dzone.com/articles/caching-best-practices
- http://tutorials.jenkov.com/software-architecture/caching-techniques.html