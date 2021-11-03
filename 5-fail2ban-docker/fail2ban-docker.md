1. Create a folder fail2ban and create the docker-compose.yml adding the following code:

```
version: "3.7"
services:
  fail2ban:
    image: crazymax/fail2ban:latest
    container_name: fail2ban_docker
    network_mode: "host"
    environment:
      - TZ=US/Eastern
      - F2B_LOG_TARGET=STDOUT
      - F2B_LOG_LEVEL=INFO
      - F2B_DB_PURGE_AGE=1d
    cap_add:
      - NET_ADMIN
      - NET_RAW
    volumes:
      - "path/to/storage/fail2ban/data:/data"
      - "path/to/storage/fail2ban/log/:/var/log/"
      - "path/to/storage/nginxproxymanager/AppData/data/logs:/log/npm/:ro"
	  - "path/to/storage/emby/logs:/log/emby/:ro"
    restart: unless-stopped
```

2. In the fail2ban/data/ folder you created in your storage, create action.d, jail.d, filter.d folders and copy the files in the corresponding folder of git into them.

i.e jail.d will have npm-docker.local,emby.local, filter.d will have npm-docker.conf,emby.conf and filter.d will have docker-action.conf,emby-action.conf respectively 

3. Once these are set, run the docker compose and check if the container is up and running or not

4. Now try going to your subdomain and entering wrong credentials, you should see the fail2ban blocking IP for 24 hours, you can use iptable commands to unblock your ip again.

Follow these guides for step to step descritpion and checking iptable regex etc.:

https://github.com/jc21/nginx-proxy-manager/issues/39#issuecomment-907795521 - setup

https://www.the-lazy-dev.com/en/install-fail2ban-with-docker/ - iptable commands etc ..

https://r-pufky.github.io/docs/services/fail2ban/setup-docker.html

