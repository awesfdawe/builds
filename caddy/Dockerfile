FROM caddy:2.10.2-builder-alpine AS builder

RUN xcaddy build \
    --with github.com/lucaslorentz/caddy-docker-proxy/v2 \
    --with github.com/caddy-dns/cloudflare

FROM caddy:2.10.2-alpine

ENV XDG_CONFIG_HOME=/config
ENV XDG_DATA_HOME=/data

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

WORKDIR /srv

CMD ["caddy", "docker-proxy"]