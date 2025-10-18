# builds

Personal builds.

### Caddy

Caddy container built with [caddy-docker-proxy](https://github.com/lucaslorentz/caddy-docker-proxy) and [cloudflare-dns](https://github.com/caddy-dns/cloudflare) plugins

```yaml
services:
  caddy:
    container_name: caddy
    image: ghcr.io/awesfdawe/caddy:latest
    restart: unless-stopped
    ports:
      - '80:80'
      - 443:443/tcp
      - 443:443/udp
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /mnt/docker-volumes/caddy/data:/data
    environment:
      - CADDY_INGRESS_NETWORKS=proxy
    networks:
      - proxy
    labels:
      - caddy.acme_dns=cloudflare ${API_KEY} # DNS:Edit permission needed
      - caddy_0=*.${DOMAIN}
      - caddy_0.respond=404

networks:
  proxy:
    external: true
```

```env
API_KEY=aadsaskdkasdaksdkadkadkaskdaksdad
DOMAIN=i.example.com
```
