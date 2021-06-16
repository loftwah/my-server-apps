version: '2.1'
services:
  hammond:
    image: akhilrex/hammond
    container_name: hammond
    volumes:
      - /path/to/config:/config
      - /path/to/data:/assets
    ports:
      - 3000:3000
    restart: unless-stopped
   docker-compose up -d

   Environment Variables
Name	Description	Default
JWT_SECRET	The secret used to sign the JWT token. There is a default value but it is important that you change it to something else	A super strong secret that needs to be changed
PORT	Change the internal port of the application. If you change this you might have to change your docker configuration as well	(empty)

docker run -d -p 3000:3000 --name=hammond -v "/host/path/to/assets:/assets" -v "/host/path/to/config:/config"  akhilrex/hammond