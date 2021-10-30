1. For this Config We can't use the Portainer as it doesn't support 3.1 at this time.

2. You need to create the following files in a custom directory you created eg: mkdir nginx

3. Create the following files in the directory:

docker-compose.yml

```
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "changeme"
      DB_MYSQL_PASSWORD: "changeme"
      DB_MYSQL_NAME: "npm"
    volumes:
      - path/in/disk/folder/nginxproxymanager/data:/data
      - path/in/disk/folder/nginxproxymanager/letsencrypt:/etc/letsencrypt
  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'changeme'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'changeme'
      MYSQL_PASSWORD: 'changeme'
    volumes:
      - path/in/disk/folder/nginxproxymanager/sql:/var/lib/mysql
	  
```
4. replace the database name password and directory with the custom directories you create for saving logs and config for different applications.

5. Also create the following file in the same directory

```
{
  "database": {
    "engine": "mysql",
    "host": "db",
    "name": "npm",
    "user": "changeme",
    "password": "changeme",
    "port": 3306
  }
}
```
Change the user name and password

6. Run the following command

```
$sudo docker-compose up -d
```

7. Check the following path in browser and see if nginx is up or not 

http:yourraspberrypiIp:81

8. Note: Replace RASPBERRYPIIP with your raspberry pi IP address followed by port 81. Example “http:192.168.2.5:81”

http:RASPBERRYPIIP:81

The default login credentials are:

Username: admin@example.com
Password: changeme
You will be prompted to Edit the User fields. Enter your credentials and click “Save“


9. You will then be asked to change your the default current password from “changeme” to your own secure password.


10. FORWARD PORT 80 AND 443 FROM YOUR ROUTER TO YOUR RASPBERRY PI.
You will now need to port forward both ports 80 and 443 from within your Router to your Raspberry Pi’s IP address and internal ports 80 and 443.

11. There are so many different router models on the market so we recommend searching on Google “how to port forward on ROUTER MODEL NAME” to get a detailed guide for your router.

Follow this guide if you face any mariadb errors: https://www.addictedtotech.net/nginx-proxy-manager-tutorial-raspberry-pi-4/