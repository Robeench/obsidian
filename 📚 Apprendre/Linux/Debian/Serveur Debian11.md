# Installation
## ISO
Récupérer l'ISO sur le [site de Debian](https://www.debian.org/distrib/index.fr.html)

## Configuration minimale requise
[Matériel minimum pour Debian](https://www.debian.org/releases/jessie/i386/ch03s04.html.fr)

- 128M de [[RAM]]
- 2Go de disque SSD
- 1 [[CPU]]

Pour être à l'aise : 
- 2Go de [[RAM]]
- 12Go de disque SSD
- 1 [[CPU]]

## Connexion réseau
Une connexion à internet est nécessaire lors de l'installation. 

## Mise à jour

``` shell
apt update && apt full-upgrade -y
```

## Nommage
Nommer mon serveur, avec une nomenclature cohérente, type : 
SRV1-ROLES

Ou, si c'est une machine cliente : 
DESKTOP01

## Configuration

``` shell
#Changer l'adresse IP de dhcp à static
nano /etc/network/interfaces
	#Mettre à minima cette config pour un passage en static
	auto ens33
    iface ens33 inet static
        address 192.168.X.X/24
        gateway 192.168.Y.Z 
	#puis recharger les paramètres réseaux
ifdown ens33
ifup ens33

#Changer le nom de la machine
nano /etc/hostname
reboot

#Changer le résolveur DNS + domaine
nano /etc/resolv.conf
	domain nitou.lan
	search nitou.lan
	nameserver 192.168.1.118
nano /etc/nsswitch.conf
#changer la ligne hosts en : 
hosts: files dns wins
```

## Vérifications

``` shell
#Connaitre les informations réseaux de la VM
ip a

#Vérifier la connexion réseau
ping 1.1

#Vérifier la connexion DNS
ping google.com

#Qui suis-je ?
pwd
whoami

#Lister les éléments de mon emplacement
ls -la

#Vérifier les dépots
/etc/apt/sources.list
```

## Installation softs / binaires 

``` shell
#Connexion en SSH de la machine hôte
ssh user@192.168.1.2

#Installation des binaires
apt install nmap zip curl net-tools dnsutils bsdgames winbind samba

#Vérification des softs installés
dpkg -l

```

## Installation Webmin

[Site officiel de Webmin](https://www.webmin.com/)
[Lien wikipedia](https://fr.wikipedia.org/wiki/Webmin)
 
``` shell

wget http://prdownloads.sourceforge.net/webadmin/webmin_1.979_all.deb
dpkg -i nomDuPaquet
apt -f install
```

Ensuite on se connecte sur https://adresseIPVM:10000
