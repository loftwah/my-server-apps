https://github.com/FreshRSS/FreshRSS/tree/edge/Docker

version: "3"

services:
  freshrss-db:
    image: postgres:12-alpine
    container_name: freshrss-db
    hostname: freshrss-db
    restart: unless-stopped
    volumes:
      - db:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: freshrss
      POSTGRES_PASSWORD: freshrss
      POSTGRES_DB: freshrss

  freshrss-app:
    image: freshrss/freshrss:latest
    container_name: freshrss-app
    hostname: freshrss-app
    restart: unless-stopped
    ports:
      - "8080:80"
    depends_on:
      - freshrss-db
    volumes:
      - data:/var/www/FreshRSS/data
      - extensions:/var/www/FreshRSS/extensions
    environment:
      CRON_MIN: '*/20'
      TZ: Europe/Paris

volumes:
  db:
  data:
  extensions: