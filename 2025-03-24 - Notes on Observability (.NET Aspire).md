Notes taken from the video by Anthony Shores “[Observing AI Applications from Dev to Production with .NET Aspire](https://www.youtube.com/watch?v=1h3W10M_VRE)” by the .NET team on YouTube.

## What Is Observability?

Observability is the practice of gaining a deep understanding of an application by examining its outputs and instrumenting its inner workings.

### Why Build Observable Applications?

- **Capture Critical Information:** Record as much data as possible so that when issues arise, you can “wind back the clock” and review what was happening at that moment.
- **Diagnose Performance Issues:** For example, if a customer reports slow performance, you can analyze various factors to understand what contributed to the delay.
- **Simplify Complexity:** Using session-specific traces can help distill vast log data into actionable insights.
- **Identify Trends:** Automatically notify when the application’s performance degrades after an update, allowing you to track historical trends.

## Introducing OpenTelemetry

OpenTelemetry is a **modern**, **open standard** for the observability of any application. It enables end-to-end tracing from the frontend to the backend in distributed architectures.

Your application sends traces, metrics, and logs to an OTEL collector. The collector forwards this telemetry data to an exporter for storage, and a user interface can then query the stored data for visualization.

| **Type**    | **Description**                                                                                                                                                                                                              | **Examples**                                     |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| **Traces**  | Traces are composed of “spans” (individual contexts) that can have attributes. They are typically generated through instrumentation and are **nested** (like a [flamegraph](https://www.brendangregg.com/flamegraphs.html)). | Retrieval calls, API calls, authentication calls |
| **Metrics** | Measurements captured at runtime by meters, such as CPU or available RAM.                                                                                                                                                    | Response times                                   |
| **Logs**    | Timestamped records that can be structured (with data) or unstructured (plain text).                                                                                                                                         | User queries, responses from LLMs                |

### Key Tools for Observability

- **.NET Aspire Dashboard:** Ideal for rapid, local development and quick diagnostics.
- **Grafana/Prometheus/Jaeger and SigNoz:** Robust, open-source stack options.
- **Datadog:** A comprehensive, turnkey solution available at a premium price.

|**Feature**|**SigNoz**|**.NET Aspire Dashboard**|**Datadog**|**Others (e.g., Grafana/Prometheus/Jaeger)**|
|---|---|---|---|---|
|**Deployment Model**|Self‑hosted (open‑source) with optional cloud support|Lightweight; designed for local development and short‑term diagnostics|Cloud‑based SaaS|Self‑hosted or cloud‑managed; modular deployments|
|**Pricing**|Free open‑source version with a paid Enterprise edition (cost based on telemetry volume)|Free (bundled with .NET tooling) – ideal for development use|Subscription‑based (can be costly as volume scales)|Mostly free/open‑source with enterprise options available|
|**Data Persistence**|Uses durable storage (e.g., ClickHouse) for long‑term retention|In‑memory only (data is not persisted across restarts; not recommended for production)|Long‑term data retention with customizable policies|Varies by component (Prometheus stores metrics short‑term; other tools handle longer retention)|
|**Observability Coverage**|Unified view of metrics, traces, and logs (native OpenTelemetry support)|Provides basic telemetry (metrics, logs, and tracing) for quick, local feedback|Comprehensive coverage including metrics, logs, traces, alerts, and AI‑driven insights|Separate tools for metrics (Prometheus), logs (Loki), and traces (Jaeger/Tempo); integration is required|
|**Integrations**|Built for cloud‑native applications; native OpenTelemetry integration with community‑driven plugins|Optimized for .NET applications (using OTLP and other .NET‑specific integrations); limited ecosystem|Extensive integrations across cloud providers, containers, on‑prem systems, and various third‑party services|A large ecosystem via plugins and community‑supported integrations (e.g., Grafana supports many data sources)|
|**Ease of Use**|Powerful and flexible; may require initial configuration but offers customizable dashboards and insights|Very simple and “opinionated” – excellent for local development and quick diagnostics, but lacks production features|Polished, user‑friendly UI with out‑of‑the‑box dashboards; minimal setup required for many use cases|Highly customizable UI (Grafana) but setup and integration require more manual effort|
|**Target Use‑Case**|Ideal for cloud‑native teams seeking a cost‑effective, self‑hosted observability solution without vendor lock‑in|Best suited for development environments and quick debugging within .NET applications|Enterprise and cloud‑native environments that require comprehensive, scalable, and fully managed monitoring|Organizations looking for a modular, flexible, open‑source stack tailored to specific needs|
