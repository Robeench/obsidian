# Consignes

- [ ] Configuration d'un AD local
- [ ] Importation de 100 users dans l'AD via powershell
- [ ] Récupération des 100 users via GLPI
- [ ] Création d'un serveur Debian11
- [ ] Le GLPI est installé à postériori sur votre LAMPS
- [ ] Accès via le bridge sur l'interface web de GLPI doit être possible, via un nom de domaine de l'AD (glpi.nitou.lan)
- [ ] Création d'entités sous GLPI
- [ ] Inventaire de WIN10_CLIENT1 via Fusion Inventory Agent
- [ ] Inventaire SERV_WIN_AD_DNS via Fusion Inventory Agent
- [ ] Inventaire manuel WIN10_CLIENT2
- [ ] Base de connaissances en exploitation sous GLPI
- [ ] Création d'un wrokflow de tickets
- [ ] Installation plugin dashboard
- [ ] Schéma réseau de l'infrastructure + logiciels

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
[generatedate.com](https://www.generatedata.com/) : pour créer un fichier de 100 users en .csv

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

![[Pasted image 20221021143629.png]]

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

![[Pasted image 20221021143945.png]]

![[Pasted image 20221021144131.png]]

### Liaison GLPI - Active Directory
https://rdr-it.com/glpi-liaison-avec-un-active-directory/

Pour ouvrir le port 389 :
Panneau de configuration > Système et sécurité > Pare-Feu Windows
	Paramètres avancés > Règles de trafic entrant
		Nouvelle règle
			Type de règle > Port
				...

![[Pasted image 20221021145056.png]]

![[Pasted image 20221021144525.png]]

### Workflow d'un ticket

![[Pasted image 20221021145402.png]]
![[Pasted image 20221021145433.png]]

### Ajout d'intitulés

![[Pasted image 20221021145614.png]]

### Fusion Inventory

![[Pasted image 20221021145714.png]]

![[Pasted image 20221021145922.png]]

