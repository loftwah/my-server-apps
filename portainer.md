docker-compose.yml

```yaml
version: '2'

services:
  portainer:
    image: portainer/portainer
    networks:
      - 'srv'
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - './portainer/data:/data'
    restart: always
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.portainer.rule=Host(`portainer.${SITE}`)'
      - 'traefik.http.services.portainer.loadbalancer.server.port=9000'
      - 'traefik.http.routers.portainer.middlewares=basic_auth@docker'
```