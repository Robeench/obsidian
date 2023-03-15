# Consignes
- [ ] Le réseau host-only est en classe B privé /25 dans la plage 172.16.0.0 à 172.16.31.255
- [ ] Construire un réseau host-only dans VirtualBox en n'assignant aucun [[Serveur DHCP]] à VirtualBox
- [ ] La dernière adresse possible est celle de la gateway sur la machine hôte
- [ ] L'avant dernière est celle sur [[Windows Server 2022]]
- [ ] Celle juste avant est celle du serveur apache
- [ ] La première via DHCP sera celle du poste client
- [ ] Choisir également un nom de domaine

## SRV01-ADDHCPDNS
- [ ] [[Windows Server 2022]]
- [ ] 2Go de [[RAM]]
- [ ] 50Go de disque SSD
- [ ] Installer les logiciels suivants :
	- [ ] 7zip
	- [ ] SumatraPDF
	- [ ] Notepad++
	- [ ] Firefox
- [ ] Installer le rôle DHCP sur ce serveur
- [ ] Installer le rôle AD de base
- [ ] Configurer - à minima - le [[Serveur DNS]] avec un alias www.nitou.lan sur la VM3
- [ ] Configurer un partage de fichier sur un deuxième [[Disque dur]] partitionné et nommé DATA
- [ ] Installer les Guest Additions

## DESKTOP01
- [ ] Windows 11 Enterprise
- [ ] 4Go de [[RAM]]
- [ ] 64Go de disque SSD
- [ ] Installer les logiciels suivants :
	- [ ] 7zip
	- [ ] SumatraPDF
	- [ ] Notepad++
	- [ ] Firefox
- [ ] Ajouter le poste au domaine nitou.lan
- [ ] Installer les Guest Additions

## SRV02-APACHE
- [ ] Debian 11
- [ ] 1Go de [[RAM]]
- [ ] 8Go de disque SSD
- [ ] Serveur Apache
- [ ] Installer Apache2
- [ ] Modifier la page index.html dans /var/www/html
- [ ] Pas de HTTPS

Ma VM2 doit pouvoir accéder à http://www.nitou.lan, sur ma page modifiée Apache.

# Installation

## Calcul des adresses [[IP]]
[Calcul des adresses IP](https://cric.grenoble.cnrs.fr/Administrateurs/Outils/CalculMasque/)

Je crée un réseau en classe B privée, en /25, dans la plage de 172.16.0.0 à 172.16.31.255

Masque de sous réseau = 255.255.255.128   /25
Gateway = 172.16.0.1
[[Windows]] Server (VM1) = 172.16.0.126
Serveur Apache (VM3) = 172.16.0.125
via [[DHCP]] (VM2), doit correspondre à = 172.16.0.2
Broadcast = 172.16.0.127
Adresse réseau = 172.16.0.0
Nom de domaine = nitou.lan

Première adresse disponible = 172.16.0.2
Dernière adresse disponible = 172.16.0.126

## Schéma de réseau
![[Capture 1.png]]

## VM1_WSRV2022
### Installation [[Windows]] Server 2022
- 2Go [[RAM]]
- 20Go de disque
![[Capture d’écran 2022-09-14 120801.png]]


### Installation logiciels
Avec une connexion en bridge qui me permet d'avoir un accès à internet : 
- 7zip
- SumatraPDF
- Notepad++
- Firefox
- Guest additions : [Installer les guest additions sur windows](https://lecrabeinfo.net/virtualbox-installer-les-additions-invite-guest-additions.html#sur-une-machine-virtuelle-windows)

![[Capture d’écran 2022-09-14 122608.png]]

J'installe chocolatey qui me permet d'installer les paquets directement via PowerShell

```PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

choco install 7zip -y
choco install sumatrapdf -y
choco install notepadplusplus -y
choco install firefox -y
```

### Définir le réseau host only pour mes machines
- Host Network Manager
	- supprimer le DHCP automatique de virtualbox
	- modifier l'adresse IP de ma carte réseau pour qu'elle corresponde à ma gateway

### Configuration des rôles
Je passe ma machine en mode Host Only
- définition adresse IP fixe
	ncpa.cpl
- changer le nom du poste
- gestion via la console
	mmc.exe

![[Capture d’écran 2022-09-14 135114.png]]

![[Capture d’écran 2022-09-14 123152.png]]

1. Installation et configuration AD
[Installation et configuration AD](https://vadmintic.wordpress.com/systemes-windows/installation-et-configuration/installation-et-configuration-du-role-ad-ds/)

2. Installation et configuration [[DNS]]
[Installez un serveur DNS](https://openclassrooms.com/fr/courses/2356306-prenez-en-main-windows-server/5835581-installez-un-serveur-dns#r-5950770)

Configurer serveur [[DNS]] avec un alias Apache
[Configurer un serveur DNS](https://openclassrooms.com/fr/courses/2356306-prenez-en-main-windows-server/5835581-installez-un-serveur-dns#/id/r-5950770)
   - Création d'un zone directe
Permet d'associer un nom à une adresse [[IP]], soit :
dynamitejet.kid -> 172.16.0.125

![[Capture d’écran 2022-09-14 134806.png]]

3. Installation et configuration [[DHCP]]
[Install un serveur DHCP](https://docs.microsoft.com/fr-fr/troubleshoot/windows-server/networking/install-configure-dhcp-server-workgroup)
- ajouter "new scope" qui permet de définir une plage d'adresses IP pour mon DHCP
	- activer le scope

![[Pasted image 20220917202552.png]]

### Partition de [[Disque dur]]
Création d'un [[Disque dur]] partitionné et nommé DATA
[Créer et formater une partition de disque dur](https://support.microsoft.com/fr-fr/windows/cr%C3%A9er-et-formater-une-partition-de-disque-dur-bbb8e185-1bda-ecd1-3465-c9728f7d7d2e)

![[Capture d’écran 2022-09-14 132031.png]]

### Partage de fichiers
[Partage de fichiers sur un réseau dans Windows](https://support.microsoft.com/fr-fr/windows/partage-de-fichiers-sur-un-r%C3%A9seau-dans-windows-b58704b2-f53a-4b82-7bc1-80f9994725bf)
[Protocole SMB pour les débutants](https://www.it-connect.fr/le-protocole-smb-pour-les-debutants/)
[Partager un dossier sur Windows Server](https://rdr-it.com/partager-dossier-windows-serveur/)

![[Capture d’écran 2022-09-13 212643.png]]

## VM2_W7PRO
- 32bits
- 1Go [[RAM]]
- 12Go disque

![[Capture d’écran 2022-09-14 132732.png]]

### Installation de logiciels
- 7zip
- SumatraPDF
- Notepad++
- Firefox
- GuestAdditions

![[Capture d’écran 2022-09-14 133012.png]]

### Intégration au domaine
Intégration au domaine dynamitejet.kid
Lorsque je me connecte, mes identifiants admin du serveur AD me sont demandés.

## VM3_DEBIAN
Installation debian
- 1Go [[RAM]]
- 8GO disque

![[Capture d’écran 2022-09-14 133708.png]]

### Installation Apache2
https://guillaume-cortes.fr/serveur-web-apache-debian-9/

#### Modification page type Apache
`nano /var/www/html/index.html`


![[Capture d’écran 2022-09-14 133622.png]]

### Configuration [[IP]] static
``` bash
su -
nano /etc/network/interfaces
```

```
allow-hotplug enp0s3
iface enp0s3 inet static
	address 172.16.0.125
	netmask 255.255.255.128
	gateway 172.16.0.1

```
