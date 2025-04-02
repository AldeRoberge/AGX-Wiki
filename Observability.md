### Why OpenTelemetry?

In the world of observability, big players like Datadog and New Relic offer nice solutions, but at a premium. SigNoz is a free and open source solution, but I had little luck setting it up.


#### What is OpenTelemetry (OTEL)?
A tool set, open observability framework for instrumenting, collecting and exporting telemetry data such as metrics, traces, logs and profiling.

Types of Telemetry Data:

**Grafana** – Acts as the central UI for visualizing and correlating metrics, logs, and traces :

| **Traces**  | Capture the path and duration of requests as they flow through services, helping understand latency and dependencies. | Jaeger / Zipkin |
| ----------- | --------------------------------------------------------------------------------------------------------------------- | --------------- |
| **Metrics** | Numeric measurements over time, such as CPU usage, memory consumption, or request counts                              | Prometheus      |
| **Logs**    | Record discrete events with contextual information.                                                                   | Loki            |


### What about .NET Aspire?
- .NET Aspire Dashboard is not meant for production (or is it? I get mixed signals)
- [https://learn.microsoft.com/en-us/dotnet/aspire/fundamentals/dashboard/standalone?tabs=bash](https://learn.microsoft.com/en-us/dotnet/aspire/fundamentals/dashboard/standalone?tabs=bash)
- The Aspire dashboard is limited in production because it has no storage. It holds a fixed number of events in memory.

### Is .NET Aspire meant for production?

".NET Aspire is a cloud-ready stack for building observable, production-ready, distributed applications."