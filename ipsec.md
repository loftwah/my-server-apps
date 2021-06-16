docker-compose.yml

```yaml
version: '2'

services:
  vpn:
    image: hwdsl2/ipsec-vpn-server:latest
    privileged: true
    environment:
      - 'VPN_IPSEC_PSK='
      - 'VPN_USER='
      - 'VPN_PASSWORD='
      - 'VPN_ADDL_USERS=' # space separated values
      - 'VPN_ADDL_PASSWORDS=' # space separated values
    ports:
      - '500:500'
      - '4500:4500/udp'
    restart: always
    volumes:
      - '/lib/modules:/lib/modules:ro'
```