# Content providers

<hr>

**<i>Última atualização: 07 de outubro de 2016</i>**

## Índice

1. [O que é um Content Provider](#definition)
- [Por que usar um Content Provider](#why_use)
- [Como Content Providers funcionam](#how_they_work)
	1. ContentResolver
	- Uri
	- Functions
	- Cursor
-  [Implementando um Content Provider](#implementing)
	1.  Contract
	-  Database Helper
	-  Provider
	-  CursorAdapter
	-  Loader

<hr>

## <a name="definition"></a> 1. O que é um Content Provider

Apps normalmente precisam de dados. As vezes **SharedPreferences** vai servir, caso você esteja armazenando poucos dados e que estes sejam bem simples (Como no exepmlo de armazenarmos a unidade em que a temperatura será exibida, Fahrenheit or Celsius). Se você precisa armazenar informações mais complexas, é necessária uma solução mais robusta.

Uma abordagem um tanto simples é conectar sua aplicação a um banco de dados. O Android oferece suporte para criar um banco de dados **SQLite** na pasta privada do seu aplicativo.

Uma restrição é que os dados em um database são privados e podem ser acessados somente pelo app que o criou. **ContentProviders** são a solução para esta questão. Este é uma classe localizada entre o app e o **dataSource** (neste caso o banco de dados e as classes que se comunicam diretamente com o database). Ao invés de se comunicar diretamente com o database pra lhe fornecer as 20 últimas rows ou inserir uma nova, por exemplo, você solicita ao **contentProvider** que execute esta tarefa. Então o **contentProvider** interage diretamente com o dataSource. Você pode estar se perguntando o motivo pelo qual você deveria utilizar um **contentProvider** e quais seriam as vantagens de usa-lo.

<hr>

## <a name="why_use"></a> 2. Por que usar um Content Provider

Usamos **contentProviders** para compartilharmos dados de uma forma segura e eficiente entre uma aplicação e um banco de dados. Compartilhar dados de forma segura é bastante importante quando permitimos múltiplas aplicações acessarem o banco de dados da nossa aplicação. O contentProvider também permite que outros apps acessem um banco de dados sem saber como estes estão armazenados. Isto é bastante útil se os dados vêm de mais de uma fonte, ou se decidirmos por mudar a fonte de dados em algum momento.

Conforme mudamos de uma **AsyncTask** para **SyncAdapters** e **CursorLoaders**, vemos que precisamos de um **ContentProvider** para realizar a comunicação entre eles. Além disso, se quisermos implementar widgets ou buscas no nosso app, precisaremos do **ContentProvider** para fornecer o acesso aos dados. Por enquanto estas necessidades não estão presentes nos apps que estamos desenvolvendo, mas **contentProviders** são uma best practice e o esforço de implementa-los irá valer a pena quando quando o app estiver em produção, e também é importante adquirir experiência com este conceito é bastante válido neste momento inicial.

<hr>

## <a name="how_they_work"></a> 3. Como Content Providers funcionam

### 3.1 Content Resolver

URI significa Uniform Resource Identifier. 

A URI pode identificar e/ou localizar dados. Normalmente eles seguem a seguinte estrutura:
`content://[content_authority]/[desired_data]`

Exemplo de uma **URI** usada pra retornar uma lista de palavras do **contentProvider** do dicionário de um usuário:
`content://user_dictionary/words`

### 3.2 Uri

Um **contentProvider** é um middleman entre a aplicação e o database. 

A aplicação acessa o **contentProvider** para ler ou armazenar dados. Este feito graças ao **ContentResolver**. Há vários ContentProviders nos aparelhos Android (contentProvider do alarme, calendário, e muitos outros). 

A comunicação entre as aplicações e um **contentProvider** é gerenciada por um **ContentResolver**. 

O **ContentResolver** procura por um **ContentProvider** na requisição feita pela sua aplicação, então verifica por qual **ContentProvider** sua aplicação está procurando. Este processamento é feito através de um **URI**;

### 3.3 Functions

Após conseguir acesso ao **ContentResolver**, podemos realizar chamadas no **ContentProvider** (update, delete, query, insert e bulkInsert).

|Tipo da função|Tipo do retorno|Descrição|
|--------------|---------------|---|
|`insert(...)`|Uri|Onde podemos encontrar o dado inserido|
|`bulkInsert(...)`|int|Quantas linhas foram inseridas|
|`update(...)`|int|Quantas linhas foram atualizadas|
|`delete(...)`|int|Quantas linhas foram removidas|
|`query(...)`|Cursor|Nos permite iterar sobre as linhas de dados retornadas|


Antes de avançarmos vamos ver o que acontece quando chamamos estas funções.

- Primeiro chamamos o **ContentResolver** para encontrar um ContentProvider. 

- O **ContentResolver** envia a mesma requisição recebida para o **ContentProvider** adequado, que por sua vez retorna o **ContentProvider** para o nosso app.

Uma vez que temos o provider, chamamos nele uma das funções listadas acima. O **ContentResolver** envia a chamada para o **ContentProvider**, que então faz a chamada para o database.

O database retorna o valor apropriado para o **ContentProvider**, que então passa para o **ContentResolver** e finalmente para a aplicação.

### 3.4 Cursor

Um **Cursor** é um iterator. Isso nos dá acesso aos dados de forma tabular. 

As operações que podemos executar no nosso cursor incluem: 

- Acessar colunas dos dados retornados;
- A quantidade de linhas retornadas;
- Iterar sobre o cursor;
- E mais...

Há muitas operações que podem ser executadas sobre um cursor, e elas podem ser verificadas na documentação do Android.

|_ID|version_name|description|icon|
|---|------------|-----------|----|
|1|Cupcake|cupcake is the first android release|2130837563|
|2|Donut|Donut description|2130837564|
|3|Eclair|Eclair description|2130837565|
|4|Froyo|Froyo description|2130837566|
|5|GingerBread|GingerBread description|2130837567|

<hr>


## <a name="implementing"></a> 4. Implementando um Content Provider

### 4.1 Contract

Para implementar nosso **contentProvider** precisamos começar criando um **Contract**. Nele nós declaramos o **contentAuthority** e o **baseURI** para o banco de dados.

Nele também definimos o nome da tabela e as respectivas colunas.

Por fim declaramos o **URI** especificando a localização da tabela, assim como as **URIs** para acessar o diretório de dados `CURSOR_DIR_BASE_TYPE` (0 ou muitas linhas) e única linha `CURSOR_ITEM_BASE_TYPE`.


### 4.2 Database Helper

Aqui é onde de fato criamos uma tabela no banco de dados. E também mantemos o número da versão atual do nosso banco.

Saber a versão do nosso banco de dados ajuda a gerencia-lo, uma vez que precisamos atualiza-lo quando houver alguma alteração.

### 4.3 Provider

Agora é a hora do **provider** de fato. A classe do **provider** deve estender de `ContentProvider`.

Implementar esta classe requer um `@override` das funções do `ContentProvider` que discutimos anteriormente. Além disso também iremos fazer `@override` na função `getType()`, que nos permite saber o tipo do conteúdo (`DIR` ou `ITEM`) baseado no **URI**.

Também temos que implementar um método que cria a `UriMatcher`, que nos permite determinar que tipo de requisição está sendo feita, baseado no **URI** enviado ao **contentProvider**. Ao usar o `matcher` podemos fazer as chamadas apropriadas ao database.

### 4.4 Cursor Adapter

No caso desta aplicação, queremos mostrar os dados do **contentProvider** em um `GridView` e aplicar um `loader` a ele. Isso significa que precisamos de um **CursorAdapter**, uma vez que nosso `provider` retorna um `Cursor` quando selecionamos dados no banco.

Estender do `CursorAdapter` requer um `@override` nos métodos:

- `newView()` - Chamado quando definimos o cursor para o adapter, que irá criar a view que iremos exibir os dados.
- `bindView()` - Chamada para cada linha do cursor para continuar a atualizar a view (item) a ser exibida.


### 4.5 Loader

Por fim, se quisermos que o `loader` seja exibido, devemos implementar o `LoaderManager` e anexa-lo ao `Cursor`.

Assim teremos o `loader` em execução até que os dados sejam retornados para o `cursor` e estejam prontos para serem exibidos.