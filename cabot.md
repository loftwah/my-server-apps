Using docker-compose
You can set up a complete cabot stack easily using docker-compose.

Clone the docker-cabot repository
git clone https://github.com/cabotapp/docker-cabot

Copy your cabot config to conf/production.env

Run docker-compose up -d

By default the compose file only binds on localhost. We recommend putting it behind a reverse proxy such as nginx or Caddy, but if you want you can change it to bind publicly on port 80.

There is a Caddyfile included which will automatically set up HTTPS using Let's Encrypt.