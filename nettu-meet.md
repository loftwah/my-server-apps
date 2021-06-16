https://github.com/fmeringdal/nettu-meet.git

$ cd server
# Copy .env.template secrets file and adjust them if needed
$ cp integrations/.env.template integrations/.env
# Using docker compose to spin up redis and mongodb 
$ npm run infra
# Installing server dependencies
$ npm i
# Starting server
$ npm start

$ cd frontend
$ npm i
$ npm start

# The response will give you a entrypoint / url for your meeting.
$ curl -X POST "http://localhost:5000/api/v1/meeting" -H  "authorization: nettu_meet_default_secret" -H  "Content-Type: application/json" -d "{  \"title\": \"First Nettu Meet meeting\"}"
