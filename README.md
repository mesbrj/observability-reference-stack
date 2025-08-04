# Observability Reference Stack

* **OTel SDK**: *Go, Python, Java* - OpenTelemetry SDKs for instrumentation
* **Grafana Alloy**: *OTel HTTP collector / K8s and containers runtimes logging*
* **Apache skywalking**: *Distributed APM (HTTP/OTel / agents: Go, Python, Java, Nginx Lua, K8s events)*
* **Grafana Loki**: *logging and log aggregation*
* **Prometheus**: *metrics collection, storage (time-series) / monitoring and alerting / PromQL querying*

This stack provides a comprehensive observability solution integrating logging, metrics, and distributed tracing across various programming languages and platforms. 

The OTel SDKs and Skywalking Agents facilitates instrumentation in applications. 
Apache Skywalking and Grafana Alloy provide solutions for a distributed APM with a powerful collector and processor (respectively).

Grafana Loki handles log aggregation and querying. The Grafana Alloy ensures that logs from various sources and signals are collected and processed effectively.

Prometheus serves for metrics collection, querying and alerting, ensuring that all components are monitored effectively.

***Stack (text) Diagram:***
```
                                |--------------------------------------|
                                | - Kubernetes (Pod Logs / K8s events) |
                                | - Podman / Docker (container logs)   |
                                |--------------------------------------|
                                            ^
                                            |
                                            |
|-----------------------------|    |------------------------------------------|     |-------------------------------------------------|
| OTel SDK (go, python, java) |--->|          Grafana Alloy (collector)       |     | Skywalking Agents (go, python, java, nginx lua) |
|-----------------------------|    |------------------------------------------|     |-------------------------------------------------|
                                     |           ^ Prometheus Exporter     |                                    |
                           Processed |           | Endpoint                | HTTP/OTel:                         |
                                Logs v           |                         v traces / metrics                   v
                    |-------------------|   |---------------------|   |--------------------------------------------|
                    |   Grafana Loki:   |   |    Prometheus:      |   |     Apache skywalking: Distributed APM     |
                    |   logging and     |   |  metrics,           |   |--------------------------------------------|
                    |   aggregation     |   |  time-series,       |                         ^ Prometheus Exporter
                    |-------------------|   |  alerting, PromQL   |                         | endpoint
                                            |  querying           |_________________________|
                                            |---------------------|
                                                    |
                                                    |
                                                    v
                                        |---------------------|
                                        | General Prometheus  |
                                        |     exporters       |
                                        | (infra monitoring)  |
                                        |---------------------|
```

## Implementation Examples

* [**GOdigital-book-looker**](https://github.com/mesbrj/GOdigital-book-looker) **Golang instrumentation**
    - A text and metadata extraction pipeline using [Apache Tika](https://tika.apache.org/).
    - [Minio](https://www.min.io/) S3 storage for files and Tika outputs.
    - Pub/Sub Message Architecture using the [Kafka v4](https://hub.docker.com/r/bitnami/kafka) broker.
    - Golang producer ([kafka-go](https://github.com/segmentio/kafka-go)) and consumer ([IBM/sarama](https://github.com/IBM/sarama)).
>
* **world-info-ds** (not started yet) **Golang and Java instrumentation**
    - A distributed-service for World information retrieval, processing and management (weather, clock, geolocation, local information, conversion, etc.).
    - JSON RPC Protocol using [RabbitMQ](https://www.rabbitmq.com/tutorials/tutorial-six-go) asynchronous queues for RPC communication.
    - Golang RPC client stub (RabbitMQ publisher) / [Golang fuego](https://github.com/go-fuego/fuego) Public RESTful (HATEOAS) OpenAPI (RPC service simplified abstraction for users interface/integration).
    - Golang RPC server skeleton worker (RabbitMQ subscriber). [Memcached](https://memcached.org/) for workers caching.
    - Java RPC server implementation using [Spring Boot](https://spring.io/) for Web Services, [MongoDB](https://spring.io/projects/spring-data-mongodb) for data persistence and [Hazelcast](https://hazelcast.com/community-edition-projects/downloads/) for real-time in-memory data grid and distributed caching.
