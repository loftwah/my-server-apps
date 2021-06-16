docker-compose.yml

```yaml
version: "3"

services:

  jackett:
    image: linuxserver/jackett
    ports:
      - "9117:9117"
    volumes:
      - ./.jackett:/config

  rapidbay:
    image: "hauxir/rapidbay:latest"
    environment:
      - JACKETT_HOST=jackett:9117
      - JACKETT_API_KEY=YOUR_API_KEY
    ports:
      - "5000:5000"
    links:
      - jackett
```