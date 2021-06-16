version: '2'
services:
  thelounge:
    image: thelounge/thelounge:latest
    container_name: thelounge
    ports:
      - "9000:9000"
    restart: always
    volumes:
      - ~/.thelounge:/var/opt/thelounge # bind lounge config from the host's file system

ENV stuff here https://thelounge.chat/docs/configuration

https://github.com/thelounge/thelounge-docker