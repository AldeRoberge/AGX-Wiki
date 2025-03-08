The [status page](https://status.aliengarden.com/status/main) uses [Uptime-Kuma](https://github.com/louislam/uptime-kuma/), an awesome open source status page from the same creator as [Dockge](https://github.com/louislam/dockge).


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

You can also : 

* Add links to all of the required services (wiki, test and prod servers)
* Make the status page the default page in the Uptime-Kuma settings
* Add an icon to the Status page