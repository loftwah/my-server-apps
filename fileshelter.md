# FileShelter Docker

A [Docker](https://docker.com) workflow for running [FileShelter](https://github.com/epoupon/fileshelter). This includes two Docker images:

*   A minimal [FileShelter image](https://hub.docker.com/r/paulgalow/fileshelter/) based on [Debian Buster Slim](https://hub.docker.com/_/debian/)
*   A minimal [Caddy](https://caddyserver.com/) image based on [Abiosoft's Alpine implementation](https://github.com/abiosoft/caddy-docker) to act as a web proxy with automatic TLS termination. ~This image includes the [http.ratelimit](https://caddyserver.com/docs/http.ratelimit) plugin~.

## [](#how-to-install)How to install

Clone or download this repository to your local machine or public facing server

```shell
git clone https://github.com/paulgalow/fileshelter-docker.git fileshelter
```

Make sure you have [Docker Engine](https://docs.docker.com/engine/installation/) and [Docker Compose](https://github.com/docker/compose/releases) installed on your machine.

If you're on a Mac all you need to do is installing [Docker for Mac](https://docs.docker.com/docker-for-mac/install/).

## [](#running-fileshelter-using-docker-compose)Running FileShelter using Docker Compose

### [](#local-development--testing)Local development / testing

To stand up a development environment (e.g. locally on your machine) run:

```shell
docker-compose up
```

To connect to FileShelter, just open your favorite browser and go to `http://localhost/`

### [](#public-facing--production)Public facing / production

To stand up this application on a public facing server first edit the production Caddyfile at `webproxy/Caddyfile_production` and enter your public domain name and your e-mail address for registering your TLS certificates. Make sure that your host is available publicly on ports 80 and 443 and via the domain name specified in `webproxy/Caddyfile_production`.

Then run:

```shell
docker-compose -f docker-compose.yml -f docker-compose.production.yml up -d
```