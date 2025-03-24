Notes taken from video by Anthony Shores "[Observing AI applications from Dev to Production with .NET Aspire](https://www.youtube.com/watch?v=1h3W10M_VRE)" from the dotnet team on YouTube.

### What is Observability?

Gaining a better understanding of an application by observing it's outputs and instrumenting it's inner workings.


#### Why have Observable Applications?

Try to capture as much information as possible, so when something goes wrong, you wind back the clock and see what was hapenning at that time.

For example, a customer reports that the app is slow, you can understand what factors contributed to the slow behavior of the app. 

Simplify the complexity of the app : With a session user trace, you can simplify extremely large logs.

Identify trends : notify if the app gets slower after an update (historically)


### Introducing OpenTelemetry

A **modern**, **open standard** for observability **of any application.** Trace end-to-end from frontend to backend in a distributed architecture. 

You application sends Traces, Metrics and Logs to the OTEL collector, which sends this telemetry data to an exporter, which allows to store the data. A user interface can then query this storage to display it.

| Type    | Description                                                                                                                              | Examples                                             |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Traces  | Traces are 'spans', or a context. <br>Spans can have attributes<br>They are typically created by instrumentation<br>Spans are **nested** | Retrieval calls<br>API Calls<br>Authentication calls |
| Metrics | Measurements captured at runtime, created by meters, like CPU or RAM available                                                           | Response times                                       |
| Logs    | Timestamped text record, can be structured (with data) or unstructured (just text)                                                       | User queries<br>Response from LLMs                   |




### Considerations for Observability in Production vs Dev






About .NET Aspire

You can run the .NET Aspire dashboard independently. 


docker run -rm -it -p 18888:1888 -p 3772:3874 -d --name aiwdadwuj





* .NET Aspire Dashboard : Good for rapid lcoal development
* Grafana/Prometheus/Jaeger and SigNoz : Robust open-source stack
* Datadog : Extensive, turnkey solution at a premium price


| **Feature**                | **SigNoz**                                                                                                       | **.NET Aspire Dashboard**                                                                                    | **Datadog**                                                                                               | **Others (e.g., Grafana/Prometheus/Jaeger)**                                                            |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Deployment Model**       | Self‑hosted (open‑source) with optional cloud support                                                            | Lightweight; designed for local development and short‑term diagnostics                                       | Cloud‑based SaaS                                                                                          | Self‑hosted or cloud‑managed; modular deployments                                                       |
| **Pricing**                | Free open‑source version with a paid Enterprise edition (cost based on telemetry volume)                         | Free (bundled with .NET tooling) – ideal for dev use only                                                    | Subscription‑based (can be costly, especially as volume scales)                                           | Mostly free/open‑source with enterprise options available                                               |
| **Data Persistence**       | Uses durable storage (e.g., ClickHouse) for long‑term retention                                                  | In‑memory only (data is not persisted across restarts; not recommended for production)                       | Long‑term data retention with customizable retention policies                                             | Varies by component (Prometheus stores metrics short‑term; other tools handle longer retention)         |
| **Observability Coverage** | Unified view of metrics, traces, logs (native OpenTelemetry support)                                             | Provides basic telemetry (metrics, logs, and tracing) focused on quick local feedback                        | Comprehensive coverage including metrics, logs, traces, alerts, and AI‑driven insights                    | Separate tools for metrics (Prometheus), logs (Loki) & traces (Jaeger/Tempo); integration needed        |
| **Integrations**           | Built for cloud‑native apps; native OpenTelemetry integration; community‑driven plugins                          | Optimized for .NET applications (using OTLP and other .NET‑specific integrations); limited ecosystem         | Extensive integrations across cloud providers, containers, on‑prem systems, and many third‑party services | Large ecosystem via plugins and community‑supported integrations (Grafana supports many data sources)   |
| **Ease of Use**            | Powerful and flexible; may require initial configuration but offers customizable dashboards and insights         | Very simple and “opinionated” – excellent for local dev and quick diagnostics, but lacks production features | Polished, user‑friendly UI with out‑of‑the‑box dashboards; minimal setup required for many use cases      | Highly customizable UI (Grafana) but setup and integration require more manual effort                   |
| **Target Use‑Case**        | Ideal for cloud‑native teams wanting a cost‑effective, self‑hosted observability solution without vendor lock‑in | Best suited for development environments and quick debugging within .NET applications                        | Enterprise and cloud‑native environments that need comprehensive, scalable, and fully managed monitoring  | Organizations looking for a modular, flexible, open‑source stack that can be tailored to specific needs |
