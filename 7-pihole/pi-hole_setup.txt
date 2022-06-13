1. For setting up pi-hole, we will be creating a vlan which we will be using for the whole network. 

2. To create a vlan, please use the below command, here we need to create a subnet with CID 24 and we use the Internet gateway, in below example we have subnet of 10.101.10.28 and the gateway is 10.10.10.1:

```
docker network create -d macvlan \
    --subnet=10.10.10.28/24 \
    --gateway=10.10.10.1 \
    -o parent=eth0 pihole_net
```

3. If you have docker portainer, open stacks section and create a new stack, run and start it or create your own docker compose yml in a directory and run docker docker-compose up -d
