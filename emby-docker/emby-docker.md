1. Login to Portainer using your credentials

2. Once logged in, In the Local, go to Stacks and add a new stack as below:

```
--- 
services: 
  emby: 
    container_name: emby
    environment: 
      - PUID=1001
      - PGID=100
      - TZ=US/Eastern
      - UNMASK=022
    image: "linuxserver/emby"
    network_mode: bridge
    ports: 
      - "8096:8096"
      - "8920:8920"
    restart: unless-stopped
    volumes:
      - /srv/dev-disk-by-uuid-3f0a28b0-c4c7-4c1d-b34a-7609f60ac241/Data/Config:/config #PrimarySSD
      - /srv/dev-disk-by-uuid-3f0a28b0-c4c7-4c1d-b34a-7609f60ac241/Data/Movies:/data/movies #PrimarySSD
      - /srv/dev-disk-by-uuid-3f0a28b0-c4c7-4c1d-b34a-7609f60ac241/Data/Photos:/data/photos #PrimarySSD
      - /srv/dev-disk-by-uuid-cc6fd87a-1e94-4440-bf81-a9aae216459a/Data/Atmos:/data/atmos #SecondarySSD
      - /srv/dev-disk-by-uuid-0297fbbf-88fe-42bb-9fe5-f8edbfad68a2/Data/MixedContent:/data/mixedcontent #FlashDrive1
      - /srv/dev-disk-by-uuid-2ac3c9e9-ee7f-4403-ac81-d1b38c841df8/Data/Animated:/data/animated #FlashDrive2
version: "2.3"

```

3. Deploy the stack and see the logs of the Container

4. If your app is not starting and failing with exit code 0 then do the following steps and deploy the stacks again.

5. First ensure you are running Raspbian buster 
 
```
    $using lsb_release -a
    Distributor ID: Raspbian
    Description: Raspbian GNU/Linux 10 (buster)
    Release: 10
    Codename: buster
```
 

6. Just run the following Command:

```
$wget http://ftp.debian.org/debian/pool/main/libs/libseccomp/libseccomp2_2.5.1-1~bpo10+1_armhf.deb

$sudo dpkg -i libseccomp2_2.5.1-1~bpo10+1_armhf.deb 

```

7. Check if emby is up by running yourraspberrylocalipaddress:8096 and setup emby
 

