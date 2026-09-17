# Observability Conventions

Production services should support the three core signals:

- Metrics
- Logs
- Traces

Where appropriate, expose:

- health status
- readiness status
- application metrics
- structured logs
- distributed tracing context

Useful baseline metrics may include:

- request count
- request duration
- error count/rate
- JVM/runtime metrics
- database connection pool usage
- Kafka consumer lag
- gRPC request latency

Prefer measurements that describe user-visible or system behavior over implementation trivia.
Avoid high-cardinality metric labels.
