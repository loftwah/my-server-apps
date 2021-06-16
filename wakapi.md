# Create a persistent volume
$ docker volume create wakapi-data

# Run the container
$ docker run -d \
  -p 3000:3000 \
  -e "WAKAPI_PASSWORD_SALT=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w ${1:-32} | head -n 1)" \
  -v wakapi-data:/data \
  --name wakapi n1try/wakapi

  config.default.yml

  env: production

server:
  listen_ipv4: 127.0.0.1              # leave blank to disable ipv4
  listen_ipv6: ::1                    # leave blank to disable ipv6
  tls_cert_path:                      # leave blank to not use https
  tls_key_path:                       # leave blank to not use https
  port: 3000
  base_path: /
  public_url: http://localhost:3000   # required for links (e.g. password reset) in e-mail

app:
  aggregation_time: '02:15'           # time at which to run daily aggregation batch jobs
  report_time_weekly: 'fri,18:00'     # time at which to fan out weekly reports (format: '<weekday)>,<daytime>')
  inactive_days: 7                    # time of previous days within a user must have logged in to be considered active
  import_batch_size: 50               # maximum number of heartbeats to insert into the database within one transaction
  custom_languages:
    vue: Vue
    jsx: JSX
    svelte: Svelte

db:
  host:                               # leave blank when using sqlite3
  port:                               # leave blank when using sqlite3
  user:                               # leave blank when using sqlite3
  password:                           # leave blank when using sqlite3
  name: wakapi_db.db                  # database name for mysql / postgres or file path for sqlite (e.g. /tmp/wakapi.db)
  dialect: sqlite3                    # mysql, postgres, sqlite3
  charset: utf8mb4                    # only used for mysql connections
  max_conn: 2                         # maximum number of concurrent connections to maintain
  ssl: false                          # whether to use tls for db connection (must be true for cockroachdb) (ignored for mysql and sqlite)
  automgirate_fail_silently: false    # whether to ignore schema auto-migration failures when starting up

security:
  password_salt:                      # change this
  insecure_cookies: true              # should be set to 'false', except when not running with HTTPS (e.g. on localhost)
  cookie_max_age: 172800
  allow_signup: true
  expose_metrics: false

sentry:
  dsn:                                # leave blank to disable sentry integration
  enable_tracing: true                # whether to use performance monitoring
  sample_rate: 0.75                   # probability of tracing a request
  sample_rate_heartbeats: 0.1         # probability of tracing a heartbeat request

mail:
  enabled: true                         # whether to enable mails (used for password resets, reports, etc.)
  provider: smtp                        # method for sending mails, currently one of ['smtp', 'mailwhale']
  sender: Wakapi <noreply@wakapi.dev>   # ignored for mailwhale

  # smtp settings when sending mails via smtp
  smtp:
    host:
    port:
    username:
    password:
    tls:

  # mailwhale.dev settings when using mailwhale as sending service
  mailwhale:
    url:
    client_id:
    client_secret:
::one::::u7121::::u7981::::skin-tone-2::::+1::::+1_1::::+1_2::::+1_3::::+1_4::::+1_5::::-1::::-1_1::::-1_2::::-1_3::::-1_4::::-1_5::::100::::1234::::clock1::::clock10::::clock11::::clock12::::clock130::::clock1030::::clock1130::::clock1230::

ENV ENVIRONMENT prod
ENV WAKAPI_DB_TYPE sqlite3
ENV WAKAPI_DB_USER ''
ENV WAKAPI_DB_PASSWORD ''
ENV WAKAPI_DB_HOST ''
ENV WAKAPI_DB_NAME=/data/wakapi.db
ENV WAKAPI_PASSWORD_SALT ''
ENV WAKAPI_LISTEN_IPV4 '0.0.0.0'
ENV WAKAPI_INSECURE_COOKIES 'true'
ENV WAKAPI_ALLOW_SIGNUP 'true'