# RabbitMQ
Based on the **A**dvanced **M**essaging and **Q**ueuing **P**rotocol that allows client side applications to communicate to compatible messaging systems;

## Definitions
Message Broker that receives messages from a publisher and forward to consumer.
They don't have to be in the same server.
Deliver ensurance by confirmation response to the `publisher`, and `ack` response from consumer to the `broker`. No messages are lost.

**Reliability**: Messages can be persisted to disk to not be lost; All message has an ack;
**MassTransit**: Use of exchanges;
**Clustering and High Availability**;
**Web interface**;
**Command line interface**;

**Producer**: a user application that sends messages;
**Queue**: a buffer that stores messages;
**Consumer**: a user application that receives messages;
**Publish/subscribe**: One message to multiple consumers;
**Binding**: Relationship between an `exchange` and a `queue`;

## Failure concerns
Duplicate messages in broker.
No `ack` received by the broker. Ending up in a redelivery. So the message must be flaged as a 'redeliver'.


## Publisher
Sends messages to a queue;

## Exchange
Middleware which the broker/brokers is binded to by a **subscription** so the message passes through it to the broker.
**Messages will be lost if no queue is binded to an exchange**;
AMQP: Introduces the `exchange` component.
Each exchange comes with 4 attributes:

- Name: The exchange name;
- Durability: Persist messages to the disk;
- Auto-delete: Delete message when not needed;
- Arguments: Message broker-dependent;
Some Types that define `exchange` behavior:
- Fanout exchange: All the messages go to all queues binded to an `exchange`;
- Direct exchange: The publisher specifies a `routing key`[ String ] so the message would go to a specific broker with a matching `bindingKey`;
- Topic exchange: Uses wildcards to specify a `binding key`.
	- `shape.*`: shape.ONE_WORD. E.g., `shape.customers`; We can also use `*.shape.*` to match `ANY.shape.ANY`;
	- `shape.#`: shape.ZERO_OR_MORE_WORDS. E.g., `shape.customers.managers` or `shape` only;
	- `shape`: shape. E.g., customers (Behaves like a `direct exchange`);
- Headers exchange: Ignore routing key. Instead, the attributes used for routing are taken from headers attributes.

## Queue
Manage queues;
Stores the messages inside queues.
Attributes:

- Name: Queue name;
- Durable: Persist the queue to disk;
- Exclusive: Delete when not needed;
- Auto delete: Deleted when consumer unsibscribes;

When a nameless queue is created, a non-durable with a random name is created. Something like `amq.gen-JzTY20BRgKO-HjmUJj0wL`;
`ch.assertQueue('', { exclusive: true });`
This queue will be deleted when its connection closes since it is declared as `exclusive`;


## Message broker
Group of exchanges and queues;

## Consumer
Might not exist at first. So the messages will keep stored in the broker until a consumer starts dequeuing them;

### Work queue/Task queue (worker)
Used to distribute time-consuming tasks among multiple workers;
Each task is delivered to exactly one worker.
Works by default in Round-robin dispatching.


## Observations
- To avoid queues and messages to be lost if rabbitMQ dies we need to mark `{ durable: true }` the queue and  `{ persistent: true }` the message;
	- It is not 100% ensured. [Morei info](https://www.rabbitmq.com/confirms.html);
- A **producer** never sends a message directly to a queue. Instead, it sends to an **exchange**;