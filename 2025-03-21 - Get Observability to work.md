---
tags:
  - telemetry
  - observability
---
In .NET, we can leverage OpenTelemetry to gather metrics, logs and traces. To visualize these traces, there exists paid solutions like Datadog and New Relics.

In the open source space, there is [SigNoz](https://signoz.io/), which seemed promising but I was unable to get to work. I tried hosting it both WSL and my Ubuntu Linux server. I could not get it to read hostmetrics.

>[!warning]
>I am waiting for an answer on my question on my [GitHub Issue](https://github.com/SigNoz/signoz/issues/7386#issuecomment-2740476567) about this subject. I hope to get SigNoz working because it looks very promising.

I now need to get Jaeger



The GitHub project [.NET with OpenTelemetry Collector](https://github.com/kimcuhoang/practical-net-otelcollector) does something very smart for observability : 

- Use [OpenTelemetry](https://opentelemetry.io/) to collect traces and metrics and [Serilog](https://serilog.net/) to collect log's messages; then all of them will only export to [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) (OTEL collector in short).
- The collector then exports to
    - [Zipkin](https://zipkin.io/) and/or [Jaeger](https://www.jaegertracing.io/) for tracings
    - [Prometheus](https://prometheus.io/) for metrics
    - [Loki](https://github.com/grafana/loki) for log's messages
- All of them are visualized on [Grafana](https://grafana.com/)

The only thing missing is that it uses Docker Compose files instead of .NET Aspire, which is a missed opportunity.

---

SigNoz has a very promising Cadvisor replacement to monitor performance of infrastructure.


---

For some god forsaken reason, it's working now. I have no clue why. Here's the setup : 


- Docker is NOT? running on Windows (nothing in the system tray)
- Docker IS running on WSL : 

```bash
demersrahp@RNWMONTEUR-2:/mnt/c/Users/demersrahp/signoz/deploy/docker/generator/infra$ docker ps
```

Produces the following output (formatted as a table for easy reading):

| CONTAINER ID | IMAGE                                        | COMMAND                | CREATED      | STATUS                  | PORTS                                                           | NAMES                 |
| ------------ | -------------------------------------------- | ---------------------- | ------------ | ----------------------- | --------------------------------------------------------------- | --------------------- |
| 62e3cf4c7bea | gliderlabs/logspout:v3.2.14                  | "/bin/logspout syslo…" | 30 hours ago | Up 14 minutes           | 80/tcp                                                          | infra-logspout-1      |
| 9f8a25ade3c9 | otel/opentelemetry-collector-contrib:0.111.0 | "/otelcol-contrib --…" | 30 hours ago | Up 14 minutes           | 4317/tcp, 55678-55679/tcp                                       | infra-otel-agent-1    |
| 37742628c44b | signoz/signoz-otel-collector:v0.111.34       | "/signoz-otel-collec…" | 30 hours ago | Up 10 minutes           | 0.0.0.0:4317-4318->4317-4318/tcp, [::]:4317-4318->4317-4318/tcp | signoz-otel-collector |
| cfd2d533f14c | signoz/signoz:v0.76.2                        | "./signoz --config=/…" | 30 hours ago | Up 14 minutes (healthy) | 0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp                     | signoz                |
| 3a82faf7e5ce | clickhouse/clickhouse-server:24.1.2-alpine   | "/entrypoint.sh"       | 30 hours ago | Up 14 minutes (healthy) | 8123/tcp, 9000/tcp, 9009/tcp                                    | signoz-clickhouse     |
| 65d56cf6625c | bitnami/zookeeper:3.7.1                      | "/opt/bitnami/script…" | 30 hours ago | Up 14 minutes (healthy) | 2181/tcp, 2888/tcp, 3888/tcp, 8080/tcp                          | signoz-zookeeper-1    |
|              |                                              |                        |              |                         |                                                                 |                       |

Notice how signoz is running.

* SigNoz is running on the admin WSL (Ubuntu)
* The Infra agent is also running on this WSL instance


My programs (that send telemetry data) are running on JetBrains Rider on Windows.

![[Pasted image 20250321152456.png]]