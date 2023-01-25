Wireguard configuration in Portainer
```
---
version: "2.1"
services:
  wireguard:
    image: lscr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Europe/Bucharest
      - SERVERURL= dynamic DNS 
      - SERVERPORT=51820
      - PEERS=2 #change to match how many devies you want to use Wireguard on
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.13.13.0 #optional
      - ALLOWEDIPS=0.0.0.0/0 #optional
    volumes:
      - /srv/dev-disk-by-uuid-bc15d92e-7e80-4922-a7c7-649f6722e505/Stocare/Containere/wireguard:/config
      - /lib/modules:/lib/modules #do not change
    ports:
      - 51820:51820/udp
    restart: unless-stopped
   ``` 
  I started by creating a stack into the Portainer and adding the above lines.
  
 The following lines need to be modified:
 
- [x] PUID&GUID (from ssh terminal, run id [username])
- [x] TZ
- [x] SERVERURL
- [x] PEERS (if needed)
- [x] volumes (only the config line)
 
 If you have a static public IP from your ISP, set the SERVERURL to auto.
 
 **If not, you can setup a Dynamic DNS that points to your Dynamic Public IP.**
 I did that using NoIP services by signing up for an account on their platform and creating a free hostname.
 
 ![image](https://user-images.githubusercontent.com/36852270/214599972-d804f45d-060b-4f9a-a8e4-9d5d6c23a3e0.png)

 After that, you need to check on your home router if you have Dynamic DNS service.
 I have 
 
  
