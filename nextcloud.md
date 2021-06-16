Upgrade
How to upgrade your Nextcloud instance:

docker-compose pull nextcloud
docker-compose stop nextcloud && docker-compose up -d nextcloud
docker-compose exec -u www-data nextcloud ./occ upgrade
To remove maintenance mode:

docker-compose exec -u www-data nextcloud php occ maintenance:mode --off

docker-compose.yml

```yaml
version: '2'

services:
  nextcloud:
    image: nextcloud
    links:
      - nextcloud-db
    volumes:
      - './nextcloud/data:/var/www/html'
    networks:
      - 'srv'
    restart: always
    healthcheck:
      test: ['CMD', 'curl', '0.0.0.0:80']
      interval: 10s
      timeout: 10s
      retries: 5
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.nextcloud.rule=Host(`nextcloud.${SITE}`)'
      - 'traefik.http.services.nextcloud.loadbalancer.server.port=80'

  nextcloud-db:
    image: mariadb
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - './nextcloud/db:/var/lib/mysql'
    environment:
      - 'MYSQL_ROOT_PASSWORD=pass'
      - 'MYSQL_PASSWORD='
      - 'MYSQL_DATABASE=nextcloud'
      - 'MYSQL_USER=nextcloud'
    restart: always
    healthcheck:
      test: ['CMD', 'mysqlcheck', '--all-databases', '-ppass']
      interval: 10s
      timeout: 10s
      retries: 5
    labels:
      - 'traefik.enable=false'
```