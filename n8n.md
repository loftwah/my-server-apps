docker run -it --rm \
	--name n8n \
	-p 5678:5678 \
	-v ~/.n8n:/home/node/.n8n \
	n8nio/n8n

N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=<USER>
N8N_BASIC_AUTH_PASSWORD=<PASSWORD>

docker run -it --rm \
	--name n8n \
	-p 5678:5678 \
	-v ~/.n8n:/home/node/.n8n \
	n8nio/n8n \
	n8n start --tunnel

docker run -it --rm \
	--name n8n \
	-p 5678:5678 \
	-e DB_TYPE=postgresdb \
	-e DB_POSTGRESDB_DATABASE=<POSTGRES_DATABASE> \
	-e DB_POSTGRESDB_HOST=<POSTGRES_HOST> \
	-e DB_POSTGRESDB_PORT=<POSTGRES_PORT> \
	-e DB_POSTGRESDB_USER=<POSTGRES_USER> \
	-e DB_POSTGRESDB_SCHEMA=<POSTGRES_SCHEMA> \
	-e DB_POSTGRESDB_PASSWORD=<POSTGRES_PASSWORD> \
	-v ~/.n8n:/home/node/.n8n \
	n8nio/n8n \
	n8n start

docker run -it --rm \
	--name n8n \
	-p 5678:5678 \
	-e DB_TYPE=mysqldb \
	-e DB_MYSQLDB_DATABASE=<MYSQLDB_DATABASE> \
	-e DB_MYSQLDB_HOST=<MYSQLDB_HOST> \
	-e DB_MYSQLDB_PORT=<MYSQLDB_PORT> \
	-e DB_MYSQLDB_USER=<MYSQLDB_USER> \
	-e DB_MYSQLDB_PASSWORD=<MYSQLDB_PASSWORD> \
	-v ~/.n8n:/home/node/.n8n \
	n8nio/n8n \
	n8n start

# Pull down the latest version from dockerhub
docker pull n8nio/n8n
# Stop current setup
sudo docker-compose stop
# Delete it (will only delete the docker-containers, data is stored separately)
sudo docker-compose rm
# Then start it again
sudo docker-compose up -d

GENERIC_TIMEZONE="Europe/Berlin"
TZ="Europe/Berlin"

https://github.com/localtunnel/localtunnel