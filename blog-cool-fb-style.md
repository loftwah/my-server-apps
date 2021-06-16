version: "3"

services:
  webserver:
    image: m1k1o/blog:latest
    container_name: blog_apache
    environment:
      TZ: Europe/Vienna
      BLOG_DB_CONNECTION: mysql
      BLOG_MYSQL_HOST: mariadb
      BLOG_MYSQL_PORT: 3306
      BLOG_MYSQL_USER: root
      BLOG_MYSQL_PASS: root
      BLOG_DB_NAME: blog
    restart: unless-stopped
    ports:
      - ${HTTP_PORT-80}:80
    volumes: 
      - ${DATA-./data}:/var/www/html/data
  mariadb:
    image: mariadb:10.1
    container_name: blog_mariadb
    environment:
      MYSQL_DATABASE: blog
      MYSQL_ROOT_PASSWORD: root
    restart: unless-stopped
    volumes:
      - mariadb:/var/lib/mysql
      - ./app/db/mysql:/docker-entrypoint-initdb.d:ro
volumes:
  mariadb: