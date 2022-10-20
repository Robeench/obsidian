# Consignes


connexion en bridge
montage LAMPS + GLPI
création AD local + DNS (pas de DHCP)
importation via script powershell de 100 utilisateurs
synchro AD / GLPI
inventaire VM WIN10 avec agent automatique
version GLPI 9.5.9 ou 10
base FAQ en exploitation
workflow de tickets d'incidents
gestion par binome des tickets
plugin dashboard
infra : schéma réseau + logiciel
je choisis mes IP
pas de dhcp sur l'ad si dhcp de ma box utilisée
mettre poste client en ip fixe

### Serveur AD + DNS
- [x] Un **AD** local sera configuré
- [ ] Un import de **100 Users** sera déposé dans l'AD via **powershell**
- [ ] Ces 100 users seront **injecté** dans le GLPI
### Serveur GLPI
- [x] Un LAMPS sous **Deb11** doit héberger la solution
- [x] Le GLPI est installé à postériori sur votre LAMPS
- [x] Un accès **via le bridge** sur l'interface web de ce GLPI doit être possible et via un nom de domaine de l'AD (glpi;nitou;lan)
- [ ] Un GLPI on-cloud général sera monté en plus sur **AWS** pour tout le monde : [https://support.cefim.ninja](https://support.cefim.ninja/)
- [ ] Une phase de "**label**" sera crée en préambule de l'exploitation des données
- [ ] **L'inventaire** d'une VM Win10 sera déposé via agent automatique dans le GLPI
- [ ] L'inventaire de l'AD également
- [ ] Une base **FAQ** & KB en exploitation
- [ ] **Workflow** de tickets d'incidents
- [ ] Gestion par binôme et dans le GLPI général des **tickets**
- [ ] Installation du plugin dashboard
### Divers
- [ ] Un schéma réseau de votre Infra

# Installation des VM

❗Si quelqu'un est connecté via un AD dans notre réseau local, il faut mettre en place un PFSense pour éviter un conflit entre les AD.

## SERV_WIN_AD
Installer mon serveur ayant le rôle AD + DNS en premier.
- définir une adresse IP fixe
- [Installation et configuration Active Directory](https://rdr-it.com/mise-en-place-environnement-active-directory/)

Si la configuration de l'AD bloque car je n'ai pas de mot de passe administrateur : 
	> ouvrir la console lusrmgr.msc
		> modifier le mot de passe du compte Administrateur (et pas d'une session avec les droits admin)
		
Accéder à la racine de la console :
[Comment ouvrir et créer une console](https://www.malekal.com/comment-ouvrir-mmc-et-creer-une-console-mmc/)
Puis ajouter une configuration DNS via : 
DNS > WIN-... > nitou.lan > clic droit > nouvel hôte A

### Import PowerShell - AD

generatedata.com : pour créer un fichier de 100 users en .csv

``` powershell
# importation du fichier users
$users = import-csv -path "C:\Users\benedicte\Documents\users.csv" -delimiter ";"

# boucle d'importation
foreach($user in $users)
{
        # variable nom et prénom
    $nom = $user.name
    $prenom= $user.surname
        # variable nom complet + id
    $nomComplet = $prenom + " " +$nom
    $idSAM = $prenom.substring(0,1) + $nom
    $id = $idSAM + "@nitou.lan"
        # xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    $pass= ConvertTo-SecureString "L'informatique ?" -AsPlaintext -Force
        # xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    New-ADuser -name $idSAM -DisplayName $nomComplet -givenname $prenom -surname $nom -Path "OU=usagers,DC=nitou,DC=lan" -UserPrincipalName $id -AccountPassword $pass -Enabled $true
}
```

## SERV_DEBIAN_GLPI
[Installation base serveur - Debian 11](obsidian://open?vault=obsidian&file=%F0%9F%96%96%20TSSR%2F3.%20G%C3%A9rer%20les%20incidents%20et%20les%20probl%C3%A8mes%2F4.%20TP%20final%2FInstallation%20base%20serveur%20-%20Debian%2011)
[TP - Installation d'un serveur web LAMP](obsidian://open?vault=obsidian&file=%F0%9F%96%96%20TSSR%2F3.%20G%C3%A9rer%20les%20incidents%20et%20les%20probl%C3%A8mes%2F2.%20GLPI%2FTP%20-%20Installation%20d'un%20serveur%20web%20LAMP)

### Changements DNS + domaine
``` shell
#Changer le nom de la machine
nano /etc/hostname

#Changer le résolveur DNS + domaine
nano /etc/resolv.conf
	domain nitou.lan
	search nitou.lan
	nameserver 192.168.1.118
nano /etc/nsswitch.conf
#changer la ligne hosts en : 
hosts: files dns wins
```


### Liaison GLPI - Active Directory
https://rdr-it.com/glpi-liaison-avec-un-active-directory/

Pour ouvrir le port 389 :
Panneau de configuration > Système et sécurité > Pare-Feu Windows
	Paramètres avancés > Règles de trafic entrant
		Nouvelle règle
			Type de règle > Port
				...