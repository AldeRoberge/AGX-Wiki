
I get the nastiest error when trying to start SigNoz using `docker compose up` on Windows.

```bash
Error response from daemon: error while creating mount source path '/run/desktop/mnt/host/c/Users/demersra/Desktop/practical-net-otelcollector/signoz/deploy/common/clickhouse/user_scripts': mkdir /run/desktop/mnt/host/c: file exists
```

The only way I was able to get SigNoz to work, was to clone the repo (like they say in the doc) and use docker compose on my Ubuntu server.


```bash
docker compose up
```

In both : 

```bash
SigNoz\signoz\deploy\docker\generator\infra\docker-compose.yaml
```

and 

```bash
SigNoz\signoz\deploy\docker\docker-compose.yaml
```

Then, you must wait quite a while. SigNoz takes about 10 minutes to boot on this pretty fast computer ; 

* Intel i9-13900KF (24 cores, 3Ghz)
* 64 Gb RAM
* NVME SSD CT500PS3SSD8
* NVIDIA RTX 4070

