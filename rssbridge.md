This guide is for people who want to run RSS Bridge using Docker. If you want to run it a simple PHP Webhost environment, see [Installation](https://github.com/RSS-Bridge/rss-bridge/wiki/Installation) instead.

## [](#setup)Setup

```shell
docker create \
--name=rss-bridge \
--volume </path/to/whitelist.txt>:/app/whitelist.txt \
--publish 3000:80 \
rssbridge/rss-bridge:latest
```

And access it using `http://IP_Address:3000`. If you'd like to run a specific version, you can run it by:

```shell
docker create \
--name=rss-bridge \
--volume </path/to/whitelist.txt>:/app/whitelist.txt \
--publish 3000:80 \
rssbridge/rss-bridge:$version
```

Where you can get the versions published to Docker Hub at [https://hub.docker.com/r/rssbridge/rss-bridge/tags/](https://hub.docker.com/r/rssbridge/rss-bridge/tags/). The server runs on port 80 internally, and you can publish it on a different port (change 3000 to your choice).

You can run it using a `docker-compose.yml` as well:

```yaml
version: '2'
services:
  rss-bridge:
    volumes:
      - ./whitelist.txt:/app/whitelist.txt
    build:
      context: .
    image: rssbridge/rss-bridge:latest
    ports:
      - 3000:80
    restart: unless-stopped
```

You can save this file as `docker-compose.yml`, create a `whitelist.txt` file next to it (just leave the file empty) before running it using `docker-compose up`. Once it gets running, you can edit the `whitelist.txt` [as per the plugins you want to run](https://github.com/RSS-Bridge/rss-bridge/wiki/Whitelisting).

# [](#container-access-and-information)Container access and information

| Function | Command |
| --- | --- |
| Shell access (live container) | `docker exec -it rss-bridge /bin/sh` |
| Realtime container logs | `docker logs -f rss-bridge` |

# [](#adding-custom-bridges)Adding custom bridges

If you want to add a bridge that is not part of [`/bridges`](https://github.com/RSS-Bridge/rss-bridge/tree/master/bridges), you can specify an additional layer to copy necessary files to the `rss-bridge` container.

*Here **root** is folder where `docker-compose.yml` and `whitelist.txt` reside.*

1.  Create `bridges` folder in root, copy your [bridges files](https://github.com/RSS-Bridge/rss-bridge/wiki/How-to-create-a-new-Bridge) there, and edit `whitelist.txt` to allow new bridges.
2.  Add `dockerfile: Dockerfile` line under `build` section to `docker-compose.yml` (from the above).
3.  Create `Dockerfile` in root:

```dockerfile
FROM rssbridge/rss-bridge:latest

COPY ./bridges /app/bridges
```

4.  Run `docker-compose up` to recreate service.