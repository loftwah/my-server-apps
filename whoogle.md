---
version: "3"

services:
  whoogle-search:
    image: benbusby/whoogle-search
    container_name: whoogle-search
    restart: unless-stopped
    ports:
      - 3123:5000
