# Implementation Examples

- https://github.com/mesbrj/OAuth2-Knowledge-Base

# Observability Reference Stack (1)

* **OTel SDK**: *OpenTelemetry SDK and API for instrumentation*
* **Grafana Alloy**: *OTel HTTP collector / K8s and containers runtimes logging*
* **Apache skywalking**: *Distributed APM*
* **Grafana Loki**: *logging and log aggregation*
* **Prometheus**: *metrics collection, storage (time-series) / monitoring and alerting / PromQL querying*

![](/docs/observability-ref.png)

This stack provides a comprehensive observability solution integrating logging, metrics, and distributed tracing across various programming languages and platforms. 

The OTel SDKs and Skywalking Agents facilitates instrumentation in applications. 
Apache Skywalking and Grafana Alloy provide solutions for a distributed APM with a powerful collector and processor.

Grafana Loki handles log aggregation and querying. The Grafana Alloy ensures that logs from various sources and signals are collected and processed effectively.

Prometheus serves for metrics collection, querying and alerting, ensuring that all components are monitored effectively.

---

# Observability Reference Stack (2)

Adapt the above stack to use [SigNoz APM](https://signoz.io/) in place of Apache Skywalking.
