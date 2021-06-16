Production
If you would like to run RSSMonster in production mode I recommend to run:

Update the VUE_APP_HOSTNAME inside the file client/.env. Most likely you want to remove port 3000 and point to the url where the backend will be running.
Inside the client folder build all the static files with: npm run build.
Move the dist output folder created inside the client folder to the server folder. The NodeJS server is also capable of serving out static content.
Inside the server folder: npm run start.
Docker for development
Run the following command to build all the images: docker-compose build
Run the following command to start the containers: docker-compose up
The client will be running on port 8080 and communication with the backend takes place via 3000. Make sure these ports aren't being used. The mysql database is accessible via port 3307.
Docker for production
The production version has the server and client combined into a single container. The VueJS is also compiled into an optimized version. To build this single image, run the following command: docker build -t rssmonster . Lastly you need to run the docker container. You need to provide the correct environment variables for the database server to connect to. Here's is an example: docker run -d -t -i -e NODE_ENV=production -e DB_HOSTNAME=localhost -e DB_DATABASE=rssmonster -e DB_USERNAME=rssmonser -e DB_PASSWORD=password -p 3000:3000 rssmonster