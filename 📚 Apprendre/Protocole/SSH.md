[[Port]] par défaut : 22, une bonne pratique consiste à le changer

[[Linux]] : serveur SSH
Ma machine : client

## Administration distante et sécurisée
### Connexion
```shell
ssh utilisateur@127.0.0.1

exit
```

### Changement de port
```shell
#SUR LE SERVEUR
nano /etc/ssh/sshd_config
#modifier le port au sein du fichier de configuration

#SUR LE CLIENT
ssh utilisateur@127.0.0.1 -p 2222 #j'indique le n° du port

# vérifier que mon serveur écoute sur un port différent 
ss -lntp | grep ssh
```

### Gérer l'[[IP]] d'écoute du serveur
```shell
nano /etc/ssh/sshd_config
#en dessous des 2 lignes ListenAddress commentée, ajouter 
ListenAddress 192.168.1.3 #j'indique l'IP qui écoute
ListenAddress :: #si je souhaite ajouter l'adresse IPv6, inutile si non utilisé
reboot now
```

### Connexion root via SSH
Par sécurité, il est interdit de se conneter en SSH directement en root. 
NE PAS autoriser une connexion directe root sur un environnement en production
```shell
nano /etc/ssh/sshd_config
#en dessous de la ligne PermitRootLogin commentée, ajouter
PermitRootLogin yes
reboot now
```

### Permission et interdiction de groupes/utilisateurs
allowUsers permet d'autoriser uniquement les utilisateurs listés à se connecter en SSH. Si elle n'existe pas, tous les comptes utilisateurs peuvent se connecter en SSH.
```shell
#UTILISATEUR
cd /etc/ssh
nano sshd_config
#ajouter la ligne
allowUsers nomUser1 nomUser2

#GROUPES
addgroup nomDuGroupe
usermod -a -G nomDuGroupe nomUser1 #option a pour garder les groupes auxquels l'user appartient déjà et option G pour spécifier le nouveau groupe
cd /etc/ssh
nano sshd_config
#ajouter la ligne
allowGroups ssh_allowed
```

### Gestion des logs
```shell
cd /var/log
nano auth.log #ouvre le fichier de log

```


## Transfert de fichier sécurisé
Utiliser le logiciel WinSCP : [Download WinSCP](https://winscp.net/eng/download.php)
### SCP - Secure Copy
scp est le nom d'une commande permettant d'échanger des fichiers et dossiers entre un client SSH et un serveur SSH. 

#### Entre deux machines [[Linux]]

![[ssh-scp-linux-01.jpg]]

##### Envoi d'un fichier
```bash
scp /home/mickael/data/Ficher2 root@192.168.10.131:/var/www/
#scp puis source puis destination
```

##### Télécharger un fichier
```bash
scp root@192.168.10.131:/var/www/Fichier2 /home/mickael/data
#scp puis fichier à télécharger puis destination

scp -r /home/mickael/data/ root@192.168.10.131:/var/www/
#-r permet de viser les sous-éléments de l'élément visé (tout un dossier)

scp -r -P 7256 /home/mickael/data/ root@192.168.10.131:/var/www/
#-p chiffreDuPort permet de spécifier un port différent du port 22
```

#### Avec un client [[Windows]]
Utiliser le logiciel WinSCP : [Download WinSCP](https://winscp.net/eng/download.php)

### SFTP - SSH File Transfert [[Protocole]]
S'utilise exactement comme scp, le nom de commande devient sftp. 

### SSHFS - SSH File System
Permet de monter un répertoire d'une machine [[Linux]] sur une autre. Le client le verra instantanément et pourra agir dessus comme s'il s'agissait d'un répertoire local. 

```bash
apt-get install sshfs #installer sshfs
mkdir /mnt/data
sshfs mickael@192.168.10.1:/home/mickael/data /mnt/data
#monte le répertoire /home/mickael/data de la machine 192.168.10.1 dans mon répertoire local /mnt/data
#Ce n'est pas une copie, mais un accès en direct
```

## X11 Forwarding
Effectuer un transfert graphique du serveur vers le client

![[schema-xforwarding-01-730x319.jpg]]

https://www.it-connect.fr/chapitres/deport-daffichage-avec-ssh-x11-forwarding/

## Authentification SSH par clefs
Pour une sécurité correcte, il est recommandé d'utiliser des clés de 4096 bits.

![[cle-asymetrique.png]]

```powershell
ls ~/.ssh #permet de voir les clés SSH

```

### Génération de la clef RSA 
#### [[Linux]]
```bash
ssh-keygen #génère une clef RSA de 2048 bits
ssh-keygen -b 4096 #-b permet de spécifier la taille de clef
```
#### [[Windows]]
utiliser Putty

### Envoyer la clef sur le serveur
```bash
ssh-copy-id root@192.168.240.132
```

## Tunneling et encapsulation de protocole
Un protocole non chiffré comme l'[[HTTP]] peut être encapsulé dans le protocole SSH pour passer un pare feu ou un [[Proxy]] par exemple. Il sera ensuite désencapsulé à la destination. 


## Commandes
```shell
systemctl restart sshd #redémarrer le service openSSH
systemctl reload sshd #recharger la configuration
```
