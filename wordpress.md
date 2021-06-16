docker-compose.yml

```yaml
version: '2'

services:
  wordpress:
    image: wordpress
    environment:
      - WORDPRESS_DB_HOST=wordpress-db
      - WORDPRESS_DB_USER=wordpress-user
      - WORDPRESS_DB_PASSWORD=${USERS}
      - WORDPRESS_DB_NAME=wordpress-db
    volumes:
      - ./wordpress/wordpress:/var/www/html
    depends_on:
      - wordpress-db
    links:
      - wordpress-db
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
      - 'traefik.http.routers.wordpress.rule=Host(`wordpress.${SITE}`)'
      - 'traefik.http.services.wordpress.loadbalancer.server.port=80'

  wordpress-db:
    image: mysql:5.7
    environment:
      - MYSQL_DATABASE=wordpress-db
      - MYSQL_USER=wordpress-user
      - MYSQL_PASSWORD=${USERS}
      - MYSQL_RANDOM_ROOT_PASSWORD=${USERS}
    volumes:
      - ./wordpress/db:/var/lib/mysql
    networks:
      - 'srv'
    restart: always
    healthcheck:
      test: ['CMD', 'mysqladmin', 'ping' , '-uwordpress-user', "-p'${USERS}'", '|', 'grep', 'alive']
      interval: 10s
      timeout: 10s
      retries: 5
    labels:
      - 'traefik.enable=false'
```