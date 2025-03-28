Observability setup can be confusing in .NET. There's many good options.

I'm thinking of using SigNoz, as it simplifies the traditional observability stack : grafana, otelcollector, prometheus, zipkin, loki, jaeger. Signoz replaces them all.

For some reason, I have terrible troubles trying to get SigNoz to work. Skill issue, yes. Also very frustrating.

The only way I've been able to get it to work is to use it on my Ubuntu VPS.

When running docker ps : 

We can see that *otel/opentelemetry-collector-contrib:0.111.0* is running at ports : *4317/tcp, 55678-55679/tcp*.

This means that we can send telemetry to this collector endpoint : 

http://5.181.218.248:4317/

