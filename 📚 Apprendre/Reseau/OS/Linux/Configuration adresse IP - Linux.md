[[Linux]]
# Configuration adresse IP - Linux
Un serveur doit garder la même adresse IP (pas via un serveur DHCP)

## Scan du réseau
Connaitre les adresses IP du réseau déjà utilisées : 
[Dipisoft - scan du réseau](https://www.dipisoft.com/articles.php?lng=fr&pg=2116)

## Ajout carte réseau sous VirtualBox
![[Capture d’écran 2022-02-18 110119.png]]

## Configuration [[IP]] static
```shell
ip a #afficher la configuration de mes cartes réseaux
nano /etc/network/interfaces 
#ajouter à mon fichier : 
allow-hotplug nomCarteReseau
iface nomCarteReseau inet static
        address 1.1.1.1 
        netmask 255.255.255.0  
        gateway 192.168.1.1

reboot now
ip a #vérifier que mon [[ip]] est correcte
```

