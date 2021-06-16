## Deployment

You can use the following docker-compose setup for testing locally or an actual deployment. Change `HAKA_BADGE_URL` to match the actual external endpoint of your instance.

Deploying on ARM is also possible using the `mujx/hakatime:latest-arm` or `mujx/hakatime:v1.4.1-arm` image or the dedicated Dockerfile ([`Dockerfile.arm`](https://github.com/mujx/hakatime/blob/master/Dockerfile.arm)) to build the image.

```yaml
version: "3"
services:
  server:
    container_name: hakatime
    image: mujx/hakatime:1.4.1
    environment:
      # DB settings.
      HAKA_DB_HOST: haka_db
      HAKA_DB_PORT: 5432
      HAKA_DB_NAME: test
      HAKA_DB_PASS: test
      HAKA_DB_USER: test
      # Server settings.
      # Fill out this field if the api is behind another path (e.g behind a reverse proxy).
      # This will adjust the Set-Cookie path for all the /auth related API calls.
      HAKA_API_PREFIX: ""
      # Update this with the external endpoint that you use to access hakatime.
      HAKA_BADGE_URL: "http://localhost:8080"
      HAKA_PORT: 8080
      HAKA_SHIELDS_IO_URL: "https://img.shields.io"
      HAKA_ENABLE_REGISTRATION: "true" # Toggle after you've created your account.
      # Number of hours after which inactive browser sessions will expire (login required).
      HAKA_SESSION_EXPIRY: "24"
      HAKA_LOG_LEVEL: "info" # Control the verbosity of the logger.
      HAKA_ENV: "dev" # Use a json logger for production, otherwise key=value pairs.
      HAKA_HTTP_LOG: "true" # If you want to log http requests.
      GITHUB_TOKEN: "<token>" # If you want to retrieve time spent per commit. No extra scope is required.
      # Add the following variables if you want to forward any received heartbeats to another
      # Wakatime compatible server.
      HAKA_REMOTE_WRITE_URL: "https://wakatime.com/api/v1/users/current/heartbeats.bulk"
      HAKA_REMOTE_WRITE_TOKEN: "<token>"
    ports:
      - "127.0.0.1:8080:8080"
  haka_db:
    container_name: haka_db
    image: postgres:12-alpine
    environment:
      POSTGRES_DB: test
      POSTGRES_PASSWORD: test
      POSTGRES_USER: test
    volumes:
      - deploy_db_data:/var/lib/postgresql/data

volumes:
  deploy_db_data: {}
```

To start all the services run:

```shell
$ docker-compose -f ./docker-compose-deploy.yml up
```

and navigate to [http://localhost:8080](http://localhost:8080) to access the dashboard.