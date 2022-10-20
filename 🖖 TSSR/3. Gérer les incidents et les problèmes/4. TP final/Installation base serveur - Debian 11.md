
## Installation de Debian 11 en mode texte
VM de Desbian 11.X
* RAM 2048mb
* réseau bridge
* HDD 12Gb

### Nom du Poste
* changename

### Domaine
* nitou.lan

### Compte root
- id = root
- mot de passe = root

### User
* id = ben
* mot de passe = ben

### Fin de l'installation
* pas d'interface graphique
* pas de serveur d'impression
* pas de SSH
* pas de serveur web

Valider GRUB.

## Configuration de la Baseline Server en mode CLI
via le compte **root**

### Réseau IP :
s'assurer que le poste ping une IP
`ping 1.1.1.1`

### DNS :
s'assurer que le poste ping un nom de domaine
`ping www.google.fr`

### Mise à jour du poste
Vérifier que les dépôts sont ok dans /etc/apt/sources.list
`apt update`
`apt upgrade`

### Mise en réseau du poste
`nano /etc/network/interfaces`
Mettre à minima cette conf pour un passage en IP Fixe
 ``` shell
   auto ens33
    iface ens33 inet static
        address 192.168.X.X/24
        gateway 192.168.Y.Z 
```

Recharger les paramètres réseau :
`ifdown ens33`
`ifup ens33`

changer le hostname :
`nano /etc/hostname`
`reboot`


Vérifier et changer le serveur **DNS** préféré ici le cas échéant par exemple pour celui de votre AD.
Changer également votre search et votre domain pour ajouter par exemple nitou.lan
[/etc/resolv.conf](https://wiki.archlinux.fr/resolv.conf)

``` shell
# fichier de configuration pour déterminer quel serveur DNS utiliser pour résoudre un nom de domaine
nano /etc/resolv.conf

# par exemple :
nameserver 1.1.1.1

```


### Configuration du profile bash du compte root
Se connecter en root sur la machine
Editer le fichier de préférence du shell via nano
`nano /root/.bashrc`
Décommenter les 5 lignes commencent par export et juste avant les RM
`Exit` puis connexion en root à nouveau 


### Installation des binaires utiles pour un sysadmin sur le serveur
`apt install ssh`
ensuite prise en main du poste à partir du terminal windows distant en compte user limité
`ssh user@votreip`
puis
`su -`

**les binutils :**
`apt install zip nmap curl lynx net-tools dnsutils`

installation de la couche **netbios**
`apt install winbind samba`

modifer le fichier **nsswitch** et ajouter wins à la fin de la directive **hosts**
`nano /etc/nsswitch.conf`

### Installation de webmin

**Récupérer le binaire en .deb** sur le site officiel [https://www.webmin.com/](https://www.webmin.com/)

Faire un clic droit sur le Debian Package dans la frame de gauche en haut et récupérer dans le presse papier l'adresse du paquet du genre:
[http://prdownloads.sourceforge.net/webadmin/webmin_1.990_all.deb](http://prdownloads.sourceforge.net/webadmin/webmin_1.990_all.deb)

Ensuite dans la console en mode ssh et en root et si possible dans /root
`wget http://prdownloads.sourceforge.net/webadmin/webmin_1.990_all.deb`

ensuite on commence l'installation
`dpkg -i webmin_1.990_all.deb`

L'installation bloque car il manque 4 paquets (des bibliothèques Perl) mais le programme APT sait les bibliothèques manquantes, donc on termine l'installation
`apt install -fy`

Il ne reste plus qu'à se connecter via le navigateur de votre hôte win10 sur votre serveur en mode web
https://votreip:10000 ou https://votrefqdn:10000