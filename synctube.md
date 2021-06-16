https://github.com/RblSb/SyncTube.git

SyncTube
Synchronized video viewing with chat and other features. Lightweight modern implementation and very easy way to run locally.

Default channel example: http://synctube-example.herokuapp.com/

etup (Docker)
As alternative, you can install Docker and run:
docker build -t synctube .
docker run --rm -it -p 4200:4200 -v ${PWD}/user:/usr/src/app/user synctube
(Docker container hides real local/global ips, so you need to checkout it manually)