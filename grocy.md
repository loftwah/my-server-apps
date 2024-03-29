docker-compose.yml

```yaml
version: '2.4'

services:

  nginx:
    image: "grocy/nginx:${GROCY_IMAGE_TAG}"
    build:
      args:
        GROCY_VERSION: v3.0.1
        PLATFORM: linux/amd64
      context: .
      dockerfile: Dockerfile-grocy-nginx
    depends_on:
      - grocy
    ports:
      - '127.0.0.1:80:8080'
      - '127.0.0.1:443:8443'
    read_only: true
    tmpfs:
      - /tmp
    volumes:
      - /var/log/nginx
    container_name: nginx

  grocy:
    image: "grocy/grocy:${GROCY_IMAGE_TAG}"
    build:
      args:
        GROCY_VERSION: v3.0.1
        PLATFORM: linux/amd64
      context: .
      dockerfile: Dockerfile-grocy
    expose:
      - '9000'
    read_only: true
    tmpfs:
      - /tmp
    volumes:
      - /var/log/php7
      - app-db:/var/www/data
    env_file:
      - grocy.env
    container_name: grocy

volumes:
  app-db:
```

  https://github.com/Forceu/barcodebuddy