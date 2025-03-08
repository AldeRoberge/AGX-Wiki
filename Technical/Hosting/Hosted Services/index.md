### Stack 1 : https-portal

We run [https-portal](https://github.com/SteveLTN/https-portal), a fully automated HTTP**S** server powered by Nginx and Let's Encrypt. It allows us to serve the wiki securely over SSL.

This reverse proxy points to the following hosted services :
* [[Status Page (Hosted Service)]]
* [[Wiki (Hosted Service)]]
* [[Game Services (Hosted Services)]].


```yaml
services:
  https-portal:
    image: steveltn/https-portal:1
    ports:
      - 80:80
      - 443:443
    restart: always
    networks:
      - wiki_default
      - status_default
      - agx_app_network
    environment:
      DOMAINS: status.aliengarden.com -> http://uptime-kuma:3001, wiki.aliengarden.com
        -> http://quartz:80, testing.aliengarden.com ->
        http://agx.web.server:8443
      STAGE: production
      WEBSOCKET: "true"
    volumes:
      - https-portal-data:/var/lib/https-portal
volumes:
  https-portal-data: null
networks:
  wiki_default:
    external: true
  status_default:
    external: true
  agx_app_network:
    external: true
```
