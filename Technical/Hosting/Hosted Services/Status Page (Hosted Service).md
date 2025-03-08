
```yaml

version: "3.8"
services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - ./uptime-kuma:/app/data
    ports:
      - 3001:3001
networks: {}
volumes:
  uptime-kuma-data: null

```


See [[Configuring the Reverse Proxy]] to learn how to publish this page to the web.
