## Docker

Setting up gotify/server with docker is pretty easy, you basically just have to start the docker container and you are ready to go:

Before starting gotify/server you may read the [Configuration](https://gotify.net/docs/config) if you f.ex. use a different database.

```bash
$ docker run -p 80:80 -v /var/gotify/data:/app/data gotify/server

```

there is a specific docker image for arm-7 processors (raspberry pi), named gotify/server-arm7.

```bash
$ docker run -p 80:80 -v /var/gotify/data:/app/data gotify/server-arm7

```

`/app/data` contains the database file (if sqlite is used), images for applications and cert-files (if lets encrypt is enabled). In this example the directory is mounted to `/var/gotify/data` this directory should be included in a backup.

The time zone inside the container is configurable via the `TZ` environment variable:

```bash
$ docker run -p 80:80 -e TZ="Europe/Berlin" -v /var/gotify/data:/app/data gotify/server

```

Docker Compose

```yml
version: "3"

services:
  gotify:
    image: gotify/server
    ports:
      - 8080:80
    environment:
      - GOTIFY_DEFAULTUSER_PASS=custom
    volumes:
      - "./gotify_data:/app/data"
```

GOTIFY_SERVER_PORT=80
GOTIFY_SERVER_KEEPALIVEPERIODSECONDS=0
GOTIFY_SERVER_LISTENADDR=
GOTIFY_SERVER_SSL_ENABLED=false
GOTIFY_SERVER_SSL_REDIRECTTOHTTPS=true
GOTIFY_SERVER_SSL_LISTENADDR=
GOTIFY_SERVER_SSL_PORT=443
GOTIFY_SERVER_SSL_CERTFILE=
GOTIFY_SERVER_SSL_CERTKEY=
GOTIFY_SERVER_SSL_LETSENCRYPT_ENABLED=false
GOTIFY_SERVER_SSL_LETSENCRYPT_ACCEPTTOS=false
GOTIFY_SERVER_SSL_LETSENCRYPT_CACHE=certs
# lists are a little weird but do-able (:
# GOTIFY_SERVER_SSL_LETSENCRYPT_HOSTS=- mydomain.tld\n- myotherdomain.tld
GOTIFY_SERVER_RESPONSEHEADERS="X-Custom-Header: \"custom value\""
# GOTIFY_SERVER_CORS_ALLOWORIGINS="- \".+.example.com\"\n- \"otherdomain.com\""
# GOTIFY_SERVER_CORS_ALLOWMETHODS="- \"GET\"\n- \"POST\""
# GOTIFY_SERVER_CORS_ALLOWHEADERS="- \"Authorization\"\n- \"content-type\""
# GOTIFY_SERVER_STREAM_ALLOWEDORIGINS="- \".+.example.com\"\n- \"otherdomain.com\""
GOTIFY_SERVER_STREAM_PINGPERIODSECONDS=45
GOTIFY_DATABASE_DIALECT=sqlite3
GOTIFY_DATABASE_CONNECTION=data/gotify.db
GOTIFY_DEFAULTUSER_NAME=admin
GOTIFY_DEFAULTUSER_PASS=admin
GOTIFY_PASSSTRENGTH=10
GOTIFY_UPLOADEDIMAGESDIR=data/images
GOTIFY_PLUGINSDIR=data/plugins