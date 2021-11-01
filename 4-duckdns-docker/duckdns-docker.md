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

4. Once the Nginx is up and running, In the home page click Add proxy and provide the subdomain you registered in duckdns.org, Provide the localIP and also forward port,for Emby it's 8096. Enable Block Common Exploits.

5. In the same tab, there will be SSL setting enable SSL and select create a new SSL certificate for the subdomain, the npm will create a new SSL ceritificate, also force it so it creates the SSL connection.

6. Now try to hit the subdomian using https://yoursubdomain.duckdns.org see if you are able to get a page with either forbidden or home page of emby, your npm is working.

7. Now in order to Emby to work , Go to Emby setting, in Network Enable remote connections and change the public ports to 80 for http, 443 for https. In the secure connection selection, select it's handled by reverse proxy. Try hitting the sudomain again, you should be able to get the home page.


Follow this guide for reference: https://www.youtube.com/watch?v=wrMn8sar-nA&list=PL9z5ElY5ntAZvTLNM99a2L98YMxMIqC_O&index=8
