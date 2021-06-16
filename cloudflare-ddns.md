docker-compose.yml

```yaml
version: "3.7"
services:
  cloudflare-ddns:
    image: timothyjmiller/cloudflare-ddns:latest
    container_name: cloudflare-ddns
    security_opt:
      - no-new-privileges:true
    network_mode: "host"
    environment:
      - PUID=1000
      - PGID=1000
    volumes:
      - /YOUR/PATH/HERE/config.json:/config.json
    restart: unless-stopped
```

https://github.com/timothymiller/cloudflare-ddns

config.json

{
  "cloudflare": [
    {
      "authentication": {
          "api_token": "api_token_here", 
          "api_key": {
              "api_key": "api_key_here",
              "account_email": "your_email_here"
          }
      },
      "zone_id": "your_zone_id_here",
      "subdomains": [
        "",
        "remove_or_replace_with_your_subdomain"
      ],
      "proxied": true
    },
    {
      "authentication": {
          "api_token": "api_token_here", 
          "api_key": {
              "api_key": "api_key_here",
              "account_email": "your_email_here"
          }
      },
      "zone_id": "your_zone_id_here",
      "subdomains": [
        "",
        "remove_or_replace_with_your_subdomain"
      ],
      "proxied": true
    }
  ]
}
