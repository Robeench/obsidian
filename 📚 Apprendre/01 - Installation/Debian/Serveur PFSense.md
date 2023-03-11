# Installation
## ISO
Récupérer l'ISO sur le [site de PFSense](https://www.pfsense.org/download/)

## Configuration minimale
- 1Go de RAM
- 1 CPU
- 8Go de disque SSD
- 2 cartes réseaux

## Configuration
### 2. Set interfaces IP address
Pour le WAN : 
IP WAN = 192.168.1.107 /24
Gateway = 192.168.1.1
DHCP = no
IPv6 = no

Pour le LAN :
IP LAN = 10.0.0.1
DHCP = no
IPv6 = no

### 7. Ping host
1.1.1.1, puis google.com pour vérifier que tout fonctionne.