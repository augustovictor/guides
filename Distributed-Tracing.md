# Distributed tracing in microservices

It is challenging to trace an application behavior in a microservices architecture we do not have a stack-trace since the comunication is not happening with in-memory calls.

For that we have **Distributed tracing** which provides us visibility across services by propagating **transactions**. That gives us information about **cross-process communications**.


## Concepts

### Span
Logical unit of work in the system, controlled by **events**, that has an **operation name**, **start time** and **duration**;
They can be nested and ordered to model causal relationships.
**Ex**: RPC like HTTP requests, database query, internal operations;
**Scenario**: example when we create an HTTP call to the other service we want to start and span, and we want to finish it when our response received while we can decorate it with the status code and other metadata.


### Trace
An execution path through the system, represented by one or more **spans**.
Think of it as a DAG(Directed Acyclic Graph) of spans

### Context propagation
This is what connects spans. To do so we need to share **tracing context** within and between(**parent-child relation**) processes.

Cross-process communication can happen via different channels and protocols like HTTP requests, RPC frameworks, messaging workers or something else. To share the **tracing context**, we can use meta headers. For example, in an HTTP request, we can use request headers like `X-Trace` or `Trace-Parent-ID`.

To manager a **span** lifecycle and handle **context propagation** we need to **instrument** our code to start and finish spans, decorate the spans with metadata and to connect them between different processes.

### Instrumentation
To do so we need to change every part of our app to propagate the tracing context both within and between processes.

Solution to implement this kind of instrumentation:
- [Trace](https://trace.risingstack.com/)
Or you can implement it yourself. But keep in mind that it can introduce bugs and cause performance issues.

## OpenTracing
- [OpenTracing](http://opentracing.io/)
- [Zipkin](http://zipkin.io/)
- [Jaeger](http://jaeger.readthedocs.io/en/latest/) (OpenTracing compatible)
It is a neutral vendor interface for instrumentation used to:
- Monitor transactions spanning many microservices;
- Measure latency of operations;
- Root cause analysis with span tags and logs;
- Contextualized span logs;
- Baggage propagation;
- Automatic generation of RPC metrics;


