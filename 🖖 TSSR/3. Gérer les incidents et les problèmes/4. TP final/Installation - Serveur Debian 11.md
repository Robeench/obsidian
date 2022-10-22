[Site officiel Debian](https://www.debian.org/index.fr.html)
[Tutoriel install Debian 10 via it-connect.fr](https://www.it-connect.fr/installation-debian-10-buster-pas-a-pas/)
[Tutoriel install Debian 10 via lecrabeinfo.net](https://lecrabeinfo.net/installer-linux-debian-le-guide-complet.html)
[Tutoriel install Debian 10 via malekal.com](https://www.malekal.com/installer-linux-debian/)
[Tutoriel install Debian 10 minimal server](https://www.howtoforge.com/tutorial/debian-minimal-server/)

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

## Installation de Debian 11 en mode texte
VM de Desbian 11.X
* RAM 2048mb
* réseau bridge
* HDD 12Gb

### Mise à jour système

``` shell
apt update && apt full-upgrade -y
```

### Installation softs / binaires 

``` shell
#Connexion en SSH de la machine hôte
ssh user@192.168.1.2

#Installation des binaires
apt install nmap zip curl net-tools dnsutils bsdgames winbind samba

#Vérification des softs installés
dpkg -l

```

### Installation Webmin

[Site officiel de Webmin](https://www.webmin.com/)
[Lien wikipedia](https://fr.wikipedia.org/wiki/Webmin)
 
``` shell

wget http://prdownloads.sourceforge.net/webadmin/webmin_1.979_all.deb
dpkg -i nomDuPaquet
apt -f install
```

Ensuite on se connecte sur https://adresseIPVM:10000

### Modifications

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