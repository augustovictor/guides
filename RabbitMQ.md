# RabbitMQ
Based on the **A**dvanced **M**essaging and **Q**ueuing **P**rotocol that allows client side applications to communicate to compatible messaging systems;

## Definitions
Microservices deployment flow:
- Commit changes;
- Compile code;
- Static code analysis;
- Execute tests;
- Packaging;
- Deploy to environment;
	- Normally testing env. Then promote it to production;

Communication types:
- Request/Response
- Event based

Uses for Message Queueing:
- **Decoupling**
- **Redundancy**
- **Scalability**
	- **X axis scalling (Horizontal duplication)**: Multiple instances of an app under a load balancer;
	- **Y axis scalling (Functional decomposition)**: Application decomposed in multiple services;
	- **Z axis scalling (Data partitioning)**: Commonly used to scale databases. Each server runs an identical copy of the code. Similar to x-axis but each server is responsible for a subset of the data; Some components in the system is responsible for redirecting each request to the appropriate server;
		- A common criteria for forwarding requests is the attributes of the request.Such as the primary key. And also the customer type.
- **Resiliency**
- **Delivery guarangees**
- **Ordering guarantees**
- **Buffering**
- **Asynchronous communication**

Desired properties:
- **Durability**: Messages stored somewhere;
- **Security policies**: Which apps should have access to these messages;
- **Message purging**: Queues and/or messages with TTL;
- **Message filtering**: Subscribers only see messages matching a specific criteria;
- **Delivery policies**: Messages delivered at least once or no more than once;
- **Routing policies**: In a system with many queue servers, what servers receive a message;
- **Batching policies**: If messages should be delivered immediately and if many messages should be delivered at once;
- **Queueing criteria**: When a message should be considered in a queue or has been forwarded to all queues;
- **Receipt notification**: When a publisher knows when a subscriber or all subscribers have received the message;

## Flow
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
- Durable: Persist the queue to disk; (Does not persist the messages); Brings extra overhead
- Exclusive: Delete when not needed;
- Auto delete: Deleted when consumer unsibscribes;

### Work queues
Aka Task Queues to avoid doing a resource-intensive task immediately and having to wait for it to complete.

### Bindings
The connection between an exchange and a queue; We can read the method `ch.bindExchange(q.queue, exName, '')` as This queue is interested in messages from this exchange;
Attributes:
- RoutingKey

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

## Remote Procedure Call
Pattern to remotely execute functions and wait for their result;
The RPC worker is the server;
Most used AMQP properties (out of 14):
- persistent: Persist in disk or not;
- content_type: Describe mime-type of the encoding. `application/json`, `text/plain`,  etc;
- reply_to: Used to name a callback queue;
- correlation_id: Useful to correlate RPC responses with requests;


## Observations
- To avoid queues and messages to be lost if rabbitMQ dies we need to mark `{ durable: true }` the queue and  `{ persistent: true }` the message;
	- It is not 100% ensured. [Morei info](https://www.rabbitmq.com/confirms.html);
- A **producer** never sends a message directly to a queue. Instead, it sends to an **exchange**;
- We have to handle duplicate responses ourselves on client side;