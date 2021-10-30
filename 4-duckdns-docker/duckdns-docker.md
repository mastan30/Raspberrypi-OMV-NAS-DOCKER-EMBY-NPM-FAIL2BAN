1. Login into the duckdns.org and get your subdomain, for example abc.duckdns.org and token provided in the website.

2. Using portainer stacks menu, add the following compose and run the duckdns:

```
---
version: "2.1"
services:
  duckdns:
    image: ghcr.io/linuxserver/duckdns
    container_name: duckdns
    environment:
      - PUID=1000 #optional
      - PGID=1000 #optional
      - TZ=Europe/London
      - SUBDOMAINS=subdomain1,subdomain2
      - TOKEN=token
      - LOG_FILE=false #optional
    volumes:
      - /path/to/appdata/config:/config #optional
    restart: unless-stopped

```

3. Check whether the duckdns is returning the nginx proxy manager index page.

Follow this guide for reference: https://www.youtube.com/watch?v=wrMn8sar-nA&list=PL9z5ElY5ntAZvTLNM99a2L98YMxMIqC_O&index=8