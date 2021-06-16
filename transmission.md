docker-compose.yml

```yaml
version: '2'

services:
  transmission:
    image: linuxserver/transmission:2.94-r1-ls12
    environment:
      - 'PGID=1000'
      - 'PUID=1000'
      - 'TZ=${TZ}'
    ports:
      - '51413:51413'
      - '51413:51413/udp'
    volumes:
      - './transmission/config:/config'
      - './transmission/downloads:/downloads'
      - './transmission/watch:/watch'
    networks:
      - 'srv'
    restart: always
    healthcheck:
      test: ['CMD', 'curl', '0.0.0.0:9091/transmission/web/']
      interval: 10s
      timeout: 10s
      retries: 5
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.transmission.rule=Host(`transmission.${SITE}`)'
      - 'traefik.http.services.transmission.loadbalancer.server.port=9091'
      - 'traefik.http.routers.transmission.middlewares=basic_auth@docker'
```