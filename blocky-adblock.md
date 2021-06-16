## Run with docker

### Alternative registry

Blocky docker images are deployed to DockerHub (`spx01/blocky`) and GitHub Container Registry (`ghcr.io/0xerr0r/blocky`) .

### Docker from command line

Execute following command from the command line:

`docker run --name blocky -v /path/to/config.yml:/app/config.yml -p 4000:4000 -p 53:53/udp spx01/blocky`

### Run with docker-compose

Create following `docker-compose.yml` file

`version: "2.1"
services:
  blocky:
    image: spx01/blocky
    container_name: blocky
    restart: unless-stopped
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "4000:4000/tcp"
    environment:
      - TZ=Europe/Berlin # Optional to synchronize the log timestamp with host
    volumes:
      # config file
      - ./config.yml:/app/config.yml`

and start docker container with

`docker-compose up -d`

### Advanced setup

Following example shows, how to run blocky in a docker container and store query logs on a SAMBA share. Local black and whitelists directories are mounted as volume. You can create own black or whitelists in these directories and define the path like '/app/whitelists/whitelist.txt' in the config file.

Example

`version: "2.1"
services:
  blocky:
    image: spx01/blocky
    container_name: blocky
    restart: unless-stopped
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "4000:4000/tcp" # Prometheus stats (if enabled).
    environment:
      - TZ=Europe/Berlin
    volumes:
      # config file
      - ./config.yml:/app/config.yml
      # write query logs in this volume
      - queryLogs:/logs
      # put your custom white and blacklists in these directories
      - ./blacklists:/app/blacklists/
      - ./whitelists:/app/whitelists/

volumes:
  queryLogs:
    driver: local
    driver_opts:
      type: cifs
      o: username=USER,password=PASSWORD,rw
      device: //NAS_HOSTNAME/blocky`