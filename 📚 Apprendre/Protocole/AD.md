= Active Directory

C'est un service d'annuaire [[LDAP]] pour les OS [[Windows]] utilisé pour stocker des informations relatives aux ressources réseaux sur un domaine. 
C'est une organisation hiérarchisée, centralisée et autonome d'objets classée en 3 catégories : 
- ressources (imprimantes, ordinateurs ...)
- services (courrier électronique ...)
- utilisateurs (compte utilisateur, groupes ...)

❗ Un AD ne pourra pas fonctionner sans DNS



## Contrôleur de domaine et domaine
### Modèle groupe de travail
Les postes [[Windows]] sont par défaut dans un groupe de travail "WORKGROUP".
La base d'utilisateurs est locale, appelée base SAM.
Inadapté lorsque le nombre de postes et d'utilisateurs augmente car lourd en administration.
Simple à mettre en œuvre pour le partage de fichiers entre quelques machines. 

### Modèle domaine
Nécessite la mise en place d'un domaine Active Directory sous [[Windows]] Server. 
Base d'utilisateurs, de groupes et d'ordinateurs centralisée.
Ouverture d'une session unique par utilisateur.
Administration et gestion de la sécurité centralisée.
Synchronisation de la base d'annuaire entre tous les contrôleurs de domaine (ils se répliquent entre eux à intervalles réguliers).

#### Contrôleur de domaine
Il traite les demandes d'authentification, veille à l'application des stratégies de groupe et stocke une copie de l'annuaire AD (nommée NTDS.dit). La réplication se fait via le [[Protocole]] DFSR.
Il doit rester actif et joignable depuis les postes clients. 
Il implique la création du domaine, de la forêt et du premier site.
Minimum 2 contrôleurs de domaine.

## Domaine, arbre et forêt 

![[Pasted image 20220512091144.png]]

domaine = it-connect.local
	sous-domaine = paris.it-connect.local
arbre = regroupement de plusieurs domaines (l'ensemble bleu)
forêt = regroupement de plusieurs arbres

Une forêt partage un schéma AD, un catalogue global, la communication entre les domaines est facilitée et accès aux ressources du domaine B pour l'utilisateur A. 

### Le niveau fonctionnel
Détermine les fonctionnalités des services de domaine AD. 
Si le niveau fonctionnel est défini pour [[Windows]] Server 2008, les fonctionnalités seront bridés à ce niveau. Le niveau fonctionnel est toujours adapté au plus "ancien", sinon le serveur devient inutilisable. 
Augmenter le niveau permet de débloquer de nouvelles fonctionnalités de l'AD, c'est indispensable dans le cadre d'une migration de l'AD. 
Le retour arrière est impossible !

Il y a un niveau fonctionnel pour les domaines et pour la forêt.

## Les protocoles
L'AD utilise des protocoles obligatoires pour fonctionner : [[LDAP]], [[DNS]] et [[Kerberos]].

### [[LDAP]]
voir [[LDAP]]

### [[DNS]]
Plusieurs enregistrements sont indispensables au bon fonctionnement de l'AD : 
- pour localiser le "Primary Domain Controller"
- pour localiser un contrôleur de domaine qui est un catalogue global
- pour localiser les KDC du domaine
- pour localiser les contrôleurs de domaine du domaine cible
- pour la correspondance nom / adresse [[IP]] des différents contrôleurs de domaine
- pour les contrôleurs de domaine via le GUID pour assurer la localisation dans toute la forêt

### [[Kerberos]]
Chaque contrôleur de domaine dispose d'un service de distribution de clés de sécurité, on l'appelle le centre de distributions de clés (KDC). 

#### Service d'authentification
- Ticket-Granding Ticket (TGT)
- le client demande un TGT, puis contacte le TGS
- le TGT est valide jusqu'à ce qu'il expire (réutilisable)

#### Service d'émission de ticket
- Distribution de tickets aux clients pour la connexion de la machine du domaine
- Ticket TGS

## Les attributs d'objets
Tout annuaire AD contient des instances d'objets de différentes classes, par exemple : ordinateur, contact, groupe, unité d'organisation, imprimante, utilisateur.
Par défaut l'AD contient déjà des containers. 

### Identifiants uniques
#### DN
cn=florian,ou=informatique,dc=it-connect,dc=local

cn = CommonName - Nom de l'objet final ciblé
ou = OrganizationalUnit
dc = DomainComposant - Utilisé pour indiquer le domaine cible

#### GUID
Identificateur global unique pour identifier un objet d'un annuaire AD
Il est attribué à la création d'un objet et ne change pas, codé sur 128 bits, unique au sein d'une forêt.

### Attributs indispensables
sAMAccountName = nom d'ouverture de session (obsolète)
userPrincipalName = nom pour l'ouverture de session précisant le nom de domaine local
description = description de l'objet
mail = adresse e-mail
adminCount = égal à 1 s'il s'agit d'un compte admin
displayName = nom complet qui sera affiché
givenName = Prénom
logonCount = nombre d'ouverture de session
accountExpires = date à laquelle le compte expire
ObjectSID = identifiant de sécurité unique qui permet d'identifier un objet
pwdLastSet = dernière modification du mot de passe
userAccountControl = état du compte
proxyAddresses = e-mail et alias de messagerie

D'autres attributs existent et on peut créer ces propres attributs. 

## Types de groupe
### Etendue de groupe
- Domaine local = utilisable uniquement dans le domaine dans lequel il est créé
- Globale = Utilisable dans le domaine local et tous les domaines approuvés par le domaine
- Universelle = Portée maximale puisqu'il est accessible dans l'ensemble de la forêt

### Type de groupe
- Groupe de sécurité = gère les autorisations d'accès à des ressources. Il dispose d'un identifiant de sécurité unique (SID)
- Groupe de distribution = création de listes de distribution pour la messagerie

Il est possible de convertir l'un en l'autre.

### Groupes par défaut
- groupes intégrés (built-in) = étendue locale, assigne des autorisations sur des fonctions d'administration
- groupes spéciaux = gérés exclusivement par le système et non-modifiables ("Tout le monde" "Utilisateurs authentifiés")
- groupes prédéfinis = en complément des groupes built-in. Ils ont différents niveaux d'étendues prédéfinies qu'on ne peut pas modifier

## Les différents rôles
### ADDS
Permet la mise en place des services de domaine AD.
- contrôle d'accès aux ressources, gestion des objets, authentification

### ADCS
Permet de gérer des clés et des certificats, c'est une autorité de certification d'entreprise. 

Par exemple : 
- basculer en LDAPS
- signer les cripts powershell
- [[HTTPS]] pour les applications web d'entreprise
- certificat pour le bureau à distance

### ADFS
Service de fédération qui simplifie l'accès à des applications internes ou externes. 
Mise en place d'une authentification unique (SSO = Single Sign-On)

### ADRMS
Système de gestion des droits avancés.
Augmente la sécurité des fichiers au niveau des accès, ce qui permet de mieux protéger l'information. 
Compatible avec la suite Office. 

### ADLDS
C'est un AD allégé car l'on peut créer un annuaire autonome sans créer de domaine. 
Permet de créer une base d'utilisateurs pouvant être utilisé dans le cadre d'un processus d'authentification auprès de l'annuaire [[LDAP]]. 
Ces utilisateurs ne seront pas utilisables pour mettre en place du contrôle d'accès.

## Le catalogue global
Annuaire qui regroupe des éléments provenant de l'ensemble de la forêt. 
Un contrôleur de domine avec ce rôle peut localiser un objet dans l'ensemble de la forêt.

Le premier contrôleur de domaine créé au sein du'une forêt est systématiquement catalogue global. On recommande d'en avoir 2 minimum ! 
- forêt mono-domaine : activer ce rôle sur tous les contrôleurs.
- forêt multi-domaines : définir un catalogue global au minimum sur un site lorsqu'il y a une centaine d'utilisateurs. 

Fonctions clés : 
- rechercher des objets dans la forêt
- résolution des noms principaux d'utilisateurs (UPN)
- information sur les appartenances aux groupes universels
- vérification des références d'objets inter-domaines

## Les rôles FSMO
FSMO = Flexible Single Master Operation
Détenir un rôle signifie pour un controleur de domaine qu'il est capable de réaliser une action particulière au sein de l'annuaire. 
Par défaut, le premier contrôleur de domaine du domaine détient les cinq rôles FSMO

Les rôles peuvent être répartis selon plusieurs méthodes : 
- interface graphique
- outil en ligne de commande : ntdsutil
- poweshell
- opération de seizing
- 

### Maitre d'attribution des noms de domaine
Distribue les noms de domaine aux contrôleurs de domaine. 
Rôle unique au sein de la forêt. 

### Contrôleur de schéma
Gère la strcture de l'annuaire AD. 
Rôle unique au sein de la forêt.

### Maitre RID
Attribue des pools RID aux contrôleurs de domaine pour générer les SID des futurs objets.
Rôle unique au sein d'un domaine.

### Maitre d'infrastructure
Gère les références entre plusieurs objets et leur réplication. 
Utiles lorsqu'il y a des échanges entre plusieurs domaines. 
Rôle unique au sein d'un domaine.

### Emulateur PDC
Gestion de l'heure (serveur de temps) et des mots de passe. 
Rôle unique au sein d'un domaine.

## Les relations d'approbations
Lien de confiance établie entre deux domaines AD, voire entre deux forêts AD. 

### Direction
Peut-être unidirectionnelle (dans un sens) ou bidirectionnelle (dans les deux sens)

### Transitivité
Si un domaine A approuve un domaine B et que le domaine B approuve un domaine C, alors le domaine A va approuver implicitement le domaine C. 
Se limite aux domaines. 

### Approbations prédéfinies
Créés automatiquemet lorsqu'on ajoute un sous-domaine à un domaine ou une forêt existante. 

### Approbations externes
Crée une relation d'approbation entre 2 forêts ou domaines de 2 forêts différentes, qui doit être créée par un administrateur. 

## Le partage SYSVOL
SYSVOL = System Volum
Sert à stocker les données spécifiques qui doivent être répliqués entre les contrôleurs de domaine ou accessibles par les ordinateurs clients. 
Stocké à l’emplacement C:\Windows\SYSVOL

On y trouve : 
- scripts de connexion
- stratégie de groupe (GPO)

La réplication se fait via le protocole DFSR.
domain = contient deux sous-dossiers pour stocker les GPO et scripts
policies = contient toutes les GPO du domaine
scripts = contient les scripts
staging = file d'attente des données en attente de réplication

### Réplication
Le protocole RCP over IP (remote procedures call over internet protocol) est utilisé pour répliquer la base d'annuaire.
Réplication automatique toute les heures. 
Le délai de réplication est de 5 minutes, avec une intervalle de 30 secondes lorsqu'il y a un changement. La réplication est immédiate quand on modifie des données liées à la sécurité (mot de passe, suppression compte)

![[Pasted image 20220513112542.png]]

#### RCP over IP
Réplications intrasites et intersites. Compressé ou non en fonction des cas

#### Protocole [[SMTP]]
Utilisé pour de la réplication sur des liaisons lentes avec une forte latence. 
Limité à la réplication entre deux domaines différents. 

### Gestion des sites
Importance de déclarer ses différents sites dans la console "Sites et services AD", puis créer des liens entre les sites et indiquer les adresses réseau utilisées. 
La réplication intersites a lieu toutes les 3h.

Premier site par défaut se crée automatiquement : Default-First-Site-Name




# Tutoriel
1. Renommer le serveur (device name)

![[Capture.png]]

Attention à nommer correctement mon serveur AD : 

![[Pasted image 20220519145118.png]]

2. Configurer une adresse [[IP]] fixe
[Configurer une [[IP]] fixe sur [[Windows]] Server](https://guides.proxgroup.fr/docs/vps/vps-game/configurer-une-ip-fixe-sur-windows-server/)

3. Configurer que le contrôleur de domaine est son propre serveur [[DNS]]
127.0.01 = nomenclature pour lui dire de s'interroger soi-même

4. Ajouter des PC [[Windows]] (PRO) à mon domaine
[Ajouter un PC [[Windows]] dans un domaine AD](https://www.youtube.com/watch?v=-XUO_BeGRI8)

```powershell
Add-Computer -DomainName nitou.corp
#permet d'ajouter le PC à un domaine AD
```

# Ressources
https://www.it-connect.fr/cours/notions-de-base-de-lactive-directory/




# a ajouter
 ACTIVE DIRECTORY 

*AD = LDAP (LDAPs = fonction sécurisé) = Annuaire = Annuaire d'identité*
Port AD 389 / Port LDAS 636   

![*](https://www.tranquil.it/wp-content/uploads/schema_ad-3.png)

AD => c'est une forêt => la forêt c'est le schéma qui est rempli d'attribut
Dnas cette forêt, il peut y avoir des domaines, voir des sous-domaines des domaines.   
En entreprise, pour éviter de complexifier son AD, on ne fait qu'un domaine, voir deux sous-domaines (messagerie et compte). On peut même simuler des sous-domaines pour ne pas complexifier l'AD. Grâce à cela on n'as qu'un seul et unique domaine à gérer.    
Le login côté AD s'apelle l'UPN (équivalent de l'adresse mail)
AD permet de gérer: les comptes génériques, les mdp, les groupes de sécurité, listes de diffusion, machines, serveur, GPO, BALS (implicitement c'est un compte / BALS: Boite aux lettres) générique, BALS équipements, BALS Salle.  

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS-OCq2R8laBtW6mDouVe1vXllxMTu2jQcSkbhDhEJE20WWA8HeU0BZaoO8QMWnwmD0dTM&usqp=CAU)

Les 5 étapes de l'installtion d'un magnifique serveur neuf:  
- Configurer un RAID  
- Installation Windows Server  
- Configuration carte réseau (no DHCP, tout est fixé)  
- Faire les MàJ Microsoft  
- Antivirus   

**SERVER AD sont les CONTROLEURS DE DOMAINES**  
Ils sont aussi serveurs DNS externes. 
Les bonnes pratiques:
- C'est deux serveurs par site. Un contrôleur de domaine ne doit rien faire d'autres.  
- Ils doivent être physique. A la limite, un des deux peut être virtualisé.(par exemple, sur une infra VMWare qui crash et que les deux serveur sont virtualisé, c'est la misère)  
- Le principal doit rester en physique. Il héberge les rôle FSMO.
- La réplication AD permet de se synchroniser dans les 15 minutes entre tout les contrôleurs de domaine.  

Dans le cas d'un multi site:

|Paris| |Marseille| |Lyon| |Clermont|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|DC Prinicpal / DC Secondaire| --> VPN IPSEC SITE A SITE --> |DC Secondaire / DC Secondaire| --> VPN IPSEC SITE A SITE --> |DC Secondaire / DC Secondaire| --> VPN IPSEC SITE A SITE --> |DC Secondaire / DC Secondaire|
||Replication AD dans le tunnel||Replication AD dans le tunnel||Replication AD dans le tunnel|
||Ad src 172.16.0.0/24 vers ad dest 172.30.0.0/24||Ad src 172.30.0.0/24 vers dest 172.62.0.0/24||Ad src 172.62.0.0 vers ad dest 172.16.0.0/24|

*Bonne pratique:  
Les 4 sites sont relié en VPN IPSEC site à site 
Sur de l'intersite, faire passer de la réplication AD dans le tunel  
Tout les Firewalls propose le VPN IPSEC site à site. Les configurer exterieurements (sur Paris, mettre l'Ip publique de Marseille, ainsi que les méthodes d'encryption. Il faut qu'elle soit égale des 2 côtés. Idem pour la clé secret partagée).
Mettre la même marque de firewall sur tout ces sites*

## AD SUR WINDOWS SERVEUR 2019

### Comment se structure une AD

Une arborescence AD, ses OU et ses sous-OU, dépend de l'entreprise dans laquelle on se trouve.

Un exemple d'organistaion (les bonnes pratiques)
Ne pas mettre d'espace ou de caractères spéciaux dans les noms d'OU

# GPO ET TRANSFERTS DE FICHIER

![](https://www.active-directory.info/wp-content/uploads/2016/03/annuaire-Active-Directory.jpg)

Tout ce dont on parle n'est valable que si l'entreprise n'a pas Teams ou Sharepoint

### PC Portables ou Fixes  

- Besoin du personnel
  - Environnement de Bureau
  - Données pures: 
    - Personnel
    - partagés ou communes ou collectives
  - Images / Photos
  - Favoris Internet(Edge)
Tout doit être sur le réseau ! Rien en dur sur le disque du PC

Côté GPO
- Attention : pour les entreprises passant par TEAMS ou SHAREPOINT pas besoin de GPO car centralisé via les logiciels
- Attention : les données doivent être mis sur des servers de fichiers donc sur le reseau via GPO
    - GPO = du bureau (va prendre le bureau.local et le transposer sur le server de fichier/réseau etc.)
    - Need gros servers de fichiers (baie de stockage) = disques VM pointés vers baie de stockage 
    - VM branchées sur baies en ESX (derrière le cluster ESX il n'y a que des baies de stockage) = baie connectée aux ESX
        - Avenir = hypercoinvergence (on s'affranchit des baies) = VMWare sait embarquer le stockage dans son noyau, stockage embarqué dans les clusters VSAN qui deviennent aussi baie (baie de stockahe imbriquée à VMWare, disques en full flash)
- Attention : les GPO ne proposent pas la rediurection des ressources partagées
    - (1) need script powersheel pour reconnecter le lecteur reseeau (script de connexion dans une GPO)
    - (2) vous connectez sur le compte de l'user directement le ecteur reseau des partages collectifs avec l'onglet 

**Côté serveur de fichiers**  

Grosse bête pointe vers une baie de stockage. Elle projète des volumes directement sur le serveur. Et le serveur dans l'explorateur Windows vas présenter la baie.

Sur le server de fichier: Arborescence dossiers
D: Dossiers Ultisateurs --> partagé --> Sécurité NTFS
  - Dossier individuel des utilisateurs --> Pas de partage --> Sécurité NTFS
  - Le dossier pour qu'il redescende en GPO doit s'appeller avec le SAM (S. Acompte Mail.) --> %UserName%
  - Partages --> partagé --> Sécurité NTFS

**Première GPO**  

Toujours faire ses GPO sur la dernières sous-OU.  
Oultis / Gestion des stratégies de Groupes.  

|Creer une GPO|
|:-:|
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/gpo_creer.png?raw=true)  

Clique-droit / Propriétés sur la GPO qui vient d'être créer.

|Script Powershell| |
|:-:|:-:|
| Mettre le script dans le dossier (en bas l'image), puis le chargé dans le gestionnaire. |![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/scriptshell_gpo.png?raw=true)|  

Création de notre arborescence de fichier sur le lecteur C:
- C:\Partages\DSI\Service_IT

## Sur le dossier parent DossiersUtilisateurs

Clique-droit sur le dossier Partages/Propriétés/Partage avancé pui cocher "Partager ce dossier"
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/partage_gpo.png?raw=true)  
*Ne pas oublier l'autorisation partage sinon pas de partage*
  
Clique-droit sur le dossier Partages/Propriétés/Sécurité puis coché "Partager ce dossier"
Cliquez sur "Convertir [...] sur cet objet" 

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/h%C3%A9ritage_gpo.png?raw=true)

Le truc qu'il faut mettre partout pour ne pas avoir d'emmerde
- Système: Accès machine, **INDISPENSABLE**.
- Admins du domaine (OM\Admins du domaine)
- Utilisateurs Authentifier.
- On fait ajouter/Admin, chercher par nom et on trouve "admins du domaine".

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/gpo_secu_2.jpg?raw=true)

- Ajouter/Avancée/recherche/Utilisateurs authentifiés/Et affichage

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/user_auth_gpo.png?raw=true)

## Sur le dossier enfant DSI

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/dsi_gpo_secu$.png?raw=true)

Ne pas laisser le ***CONTROLE TOTAL*** pour les utilisateurs car cela leur donne accès à l'onglet de sécurité ce qui est une faille de sécuité énorme.

## Faire la même procédure pour le dossier enfant Service_IT.

On vas s'occuper de l'arborescence des dossiers utisateurs.
- On crée le dossier à la racine du disque:
  - C:\DossiersUtilisateurs
- On applique le partage sur ce dossier (comme vu précedemment).
- Sécurité:
  - On désactive l'héritage (comme vu précédemment).
  - On active la sécurité système, administrateur du domaine et utilisateurs authentifiers.
- Dans le dossier parent, on crée un dossier enfant avec un le SAM de l'utilisateur (apendragon).  
  - On gère la sécurité(comme vu précedemment) mais on enlève l'utilisateur authentifier et mettre l'user à la place, avec les rêgles qui vont bien.

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/secu_user_gpo.png?raw=true)

## Quota
Sur C: Clique-droit/propriétés/onglet Quota: 
- Cocher Activer la gestion
-  Refuser de l'espace disque ...   

Si on rend pas l'utilisateur propriétaire de son dossier, il n'auras pas son quota.
Pour faire de l'individuel, il faut clique-droit sur l'user pour gérer son espace disque.

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/quota_gpo$.png?raw=true)

Clique-droit sur le dossier/Propriétés/Sécurité/Avancé/Modifier/Choisir l'utilisateur.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/proprio_dossier_user.png?raw=true)

## Dossiers des utilisateurs

Ouvrir l'éditeur de Gestion des stratégies de groupes 
Bureau: 
- Clique-droit/propriétés/Cible  
  - Paramêtres: *De base*
  - Rentrer le chemain d'accès à la racine \\WS19\DossiersUtilisateurs

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/proprio_bureau_gpo.png?raw=true)

- Clique-droit/propriétés/Paramètres
  - Décoché *Accorder à l'utilisateus des droits exclusifs sur Bureau* (sinon les admins ne peuvent plus y accèder pour régler des problèmes)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/proprio_bureau_gpo2.png?raw=true)

Favoris:
- Clique-droit/propriétés/Cible  
  - Paramêtres: *De base*
  - Rentrer le chemain d'accès à la racine \\WS19\DossiersUtilisateurs 

Documents:
- Clique-droit/propriétés/Cible  
  - Paramêtres: *De base*
  - Rentrer le chemain d'accès à la racine \\WS19\DossiersUtilisateurs

Images:
- Clique-droit/propriétés/Cible   
  - Paramêtres: *Suivre les documents*  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/suivre_doc_gpo.png?raw=true)  

Pour le partage colléctif:
- AD
- User / Compte Utilisateurs / Delegue / ComptesUtilisateurs
- clique-droit / Propriété / Profil / chemin d'accès local 
    - Z:\\WS19\Partages\DSI

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/partage_co_gpo.png?raw=true)

Vérification du bon fonctionnement des GPO:
- Monter un W10
- Créer un user à rattaché au Domaine (check dans computer dans l'AD pour l'arrivée)
- Mettre un fichier dans un des dossiers Documents/Images/...
- Check dans l'AD s'il apparait bien dans l'arborescence de l'AD par DossierUser

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/win10_resultat.jpg?raw=true)

**Ressources:**
- [Entretien AD](https://www.active-directory.info/comment-bien-entretenir-son-annuaire-active-directory%E2%80%89/)


# MIGRATION ACTIVE DIRECTORY 2016 vers 219 (lvl ingénieur)

***Migration de version d'AD / Passer de 2016 à 2019***

**Ressources web**
- [Docs microsoft : Installer, mettre à niveau ou migrer vers Windows Server](https://docs.microsoft.com/fr-fr/windows-server/get-started/install-upgrade-migrate)
- [System-net : Migration Windows Server 2019 : Les étapes](https://www.system-net.fr/windows-server-2019/)
- [How to: Migration to Windows Server 2019 / 2016, including applications, profiles, shares and data](https://www.zinstall.com/how-to/how-to-server-2016-migration-software-for-windows-server-2003-2008-2012)
- [Migration d’une infra simple d’un serveur Active Directory 2012R2 vers 2016](https://laboiteajb.fr/migration-dune-infra-simple-dun-serveur-active-directory-2012r2-vers-2016/)

### Elements de compréhension et étapes à suivre

*Attention : Need monter de niveau fonctionnel 2012 vers 2016 (niveau fonctionnel toujours au plus haut pour migration)*

#### Migration simple

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/IMG_20210831_172100_889.jpg)

**Existant**

| DC Principal | DC secondaire |
|:-:|:-:|
|Rôle FSMO| - |
|AD WServer 2016| AD WServer 2016|

**Préparation à la migration**

Faire venir une forêt 2019 dans une forêt 2016 = trois étapes exclusives au prinicpal (puisque possède les FSMO) pour préparation
  1. couper les réplications AD entre contollers (1 ligne de commande à passer) 
  2. préparer la forêt (1 ligne de commande à passer)
  3. prénarer le domaine (1 ligne de commande à passer)

**Première étape de migration**

- Préparation d'un WServer 2019 : NIC, antivirus etc.
- Insérer le WServer 2019 en controller de domaine secondaire dans la forêt 2016
  - Va se coller à la forêt 2016
  - Mode dit "mixte" (possible de rester ainsi en plusieus mois)
 
| DC Principal | DC secondaire | DC secondaire
|:-:|:-:|:-:|
|Rôle FSMO| - | - |
|AD WServer 2016| AD WServer 2016| AD WServer 2019|

**Seconde étape de migration**

- On migre les FSMO (les 5) doivent migrer vers DC secondaire 2019 
    - Via interface graphique

| DC secondaire | DC secondaire | DC principal
|:-:|:-:|:-:|
| - | - | Rôle FSMO |
|AD WServer 2016| AD WServer 2016| AD WServer 2019|

**Troisième étape de migration**

- Rétrogradation du second controller secondaires
    - Plus DNS ni AD
    - Redevient server simple

| DC secondaire | Server simple | DC principal
|:-:|:-:|:-:|
| - | - | Rôle FSMO |
|AD WServer 2016| AD WServer 2016| AD WServer 2019|

**Quatrième étape de migration**

- On crash/réinstalle le server simple en WServer2019
- On le fait venir en secondaire en 2019

| DC secondaire | DC secondaire | DC principal
|:-:|:-:|:-:|
| - | - | Rôle FSMO |
|AD WServer 2016| AD WServer 2019| AD WServer 2019|

- Bis repetita pour le premier controller

| DC secondaire | DC secondaire | DC principal
|:-:|:-:|:-:|
| - | - | Rôle FSMO |
|AD WServer 2019| AD WServer 2019| AD WServer 2019|

#### Migration de forêts

- Entreprise : acab.lan
- Achat ou fusion : nouveau nom, need nouvelle forêt (ex. anar.lan)
- Annunaire unique, identifiant unique à partir de plusieurs annuaires/identifiants

| Forêt 1 | Forêt 2 | > | Nouvelle forêt 1 | Nouvele forêt 2 |
|:-:|:-:|:-:|:-:|:-:|
| acab.lan | acab.lan | > | anar.lan | anar.lan |
| Controller 1 | Controller 2 | > | NvController 1 | NvController 2 |

![*](https://rdr-it.com/wp-content/uploads/2019/06/admt-00.png)

- Temps long : 
    - Mise en place DNS (Zone de stub, redirecteurs conditionnels) + relations d'approbation bi-directionnelle entre les deux domaines/forêts = permet la communication entre les deux forêts
    - Utilisation d'un [server ADMT](https://rdr-it.com/admt-outil-de-migration-de-domaine-active-directory/3/) pour la migration les objets de la source vers la cible
    - Installation de [Password Export Server](http://pbarth.fr/node/112) : utilitaire de migration des mots de passe
    - Une fois cela effectué on peut commencer à migrer
- On ne supprime les deux controllers de base qu'une fois l'ensemble de la migration effectuée


#### Migration via Azure AD

- Azure AD se base sur l'AD local
- Azure récupère et transpose directement dans Office365

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/IMG_20210831_171914_624.jpg)

| DC Principal | DC secondaire | <- AZURE AD Source -> | Office 365 |
|:-:|:-:|:-:|:-:|
|Rôle FSMO| - | - | - |
|AD WServer 2016| AD WServer 2016| - | - |
|local 2019| local 2019 | - | - |

![*](https://docs.microsoft.com/fr-fr/azure/active-directory/hybrid/media/how-to-upgrade-previous-version/stagingserver1.png)

- UPN : obligé de passer par ligne de commande 

### ON VA MANIPER - MIGRATION WINDOWS SERVEUR 2016 A WINDOWS SERVEUR 2019

Sur Windows Servuer 2016  
Ouvrir l'invite de commande dans la VM et se rendre à la racine de C.  

On coupe les réplications  
> C:\>repadmin /options WS16 +disable_outbound_repl   

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_repadmin.png?raw=true)

Pour préparer l'AD 2016 à recevoir la fôret de 2019. 
On charge l'ISO de Windows Serveur 2019 dans le lecteur virtuel.  
On se met dans le répertoire support puis adprep.  
> D:\support\aprep>

On tape la commande:  
>adprep /forestprep

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_adprep.png?raw=true)
  
Toujours dans D:\support\adprep> , on met à jour le domaine:  
>adprep /domainprep  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/_mig_domain.png?raw=true)

**Ajouter un contrôleur AD 2019 dans notre AD 2016**  

Maintenant, on peut ajouter un contrôleur AD 2019 dans notre AD 2016.  
On réactive les répliques et on y touche plus. Pas besoin de les couper à nouveau, même si on reprends la migration des mois plus tard.  
Retour dans C:
>repadmin /options WS16 -disabled_outbound_repl

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_activerepl.png?raw=true)

On monte un Windows Serveur 2019.  
On désactive le firewall et on met l'adresse du controlleur de domaine 2016 en DNS primaire.  
On prends une petite sureté, on ping les machines entre elle.  

Ensuite, il faut ajouter le Windows Serveur 2019 dans le **domaine** bobdy.lan  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_mise_domaine.png?raw=true)

**Se reconnecter dans le Windows Serveur 2019 en compte bobdy\administrateur.**

Installer les rôle AD DS.

Promouvoir en Controlleur de Domaine.
Verifier qu'on soit bien dans le bon domaine.

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/promo_control.png?raw=true)

On passe au vérifications, pour être sûr que tout c'est bien passé.
  - Dans l'AD19, Carte Réseau: mettre l'AD 2019 en DNS primaire et l'AD 2016 en DNS Secondaire.
![]()
  - Dans l'AD19, Gestionnaire DNS: Verifier qu'il y ai bien: 
    - les zones, les records et les zones inversées.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gest_dns.png?raw=true)  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gest_dn3.png?raw=true)
    - les serveurs de noms  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gest_dns2.png?raw=true)  
    - les suffixes UPN  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gest_dns4.png?raw=true)  
    - les sites and services  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gest_dns5.png?raw=true)  
  - les réplications
  - les OU et sous-OU

  - Dans l'AD 2016, dans les paramêtre de carte réseau, mettre comme DNS secondaire l'AD 2019.

**MIGRATION DES ROLES FSMO DE l'AD2016 à L'AD2019**  

Le premier rôle a migré est caché. Il faut donc le faire apparaitre via une *petite commande*. Ouvrir l'invit de commande et se renre à la racine C:\
>regsvr32 schmmgmt.dll

On vas lancer une console vierge: 
|windows + R et **mmc**|
|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/winR.png?raw=true)|

|Faire "Ajouter..fichables" puis ajouter le Schéma Active Directory|
|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/fsmo_mmc.png?raw=true)|

|Clique-droit sur "Schéma Active Directory", Changer de contrôleur de domaine Active Directory|
|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/fsmo_mmc2.png?raw=true)|

Clique-droit sur "Schéma Active Directory", Maitre d'Opérations, Cliquez sur Modifier:
|Clique-droit sur "Schéma Active Directory", Maitre d'Opérations| Cliquez sur Modifier|
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/fsmo_mmc3.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/fsmo_mmc4.png?raw=true)

**2ème ROLE**

Dans Domaines et Approbations Active Directory
Clique-droit, Changer de contrôleur de domaine Active Directory et promouvoir l'AD 2019
Clique droit, Maitre d'Opérations, Cliquez sur Modifier

**3 DERNIER ROLE**

Dans Utilisateurs et ordinateurs Active Directory
Clique-droit, Changer de contrôleur de domaine Active Directory et promouvoir l'AD 2019
Clique-droit sur notre nom de domaine, Maitre d'opérations:
  - RID : Modifier, OUI, oK
  - CDP: Modifier, OUI, ok
  - Infrastructure: Modifier, OUI, ok

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/fsmo_mmc5.png?raw=true)

**RETROGRADATION DE WINDOWS SERVEUR 2016**

Gestionnaire de Serveurs, Gérer, Supprimer des rôles et des fonctionnalités.
Il nous propose une méthode de rétrogradation à la décoche.

Décocher Service AD DS  
![](https://raw.githubusercontent.com/cromm24/Hello_World/main/AT2/AT2C1/AD/mig_retro_AD.png?raw=true)

Cocher "Procéder à la suppression"  
![](https://raw.githubusercontent.com/cromm24/Hello_World/main/AT2/AT2C1/AD/mig_retro_AD2.png?raw=true)

Cliquez sur Retrograder  
![](https://raw.githubusercontent.com/cromm24/Hello_World/main/AT2/AT2C1/AD/mig_retro_AD3.png?raw=true)

Enfin refaire supprimer les rôles et décocher les deux rôles et cette fois-ci il ne vas pas discuter.  
On va dans les paramêtres de carte réseau et on retire l'adresse IP du DNS du Windows Serveur 2016.  
![](https://raw.githubusercontent.com/cromm24/Hello_World/main/AT2/AT2C1/AD/mig_retro_AD4.png?raw=true)

**QUELQUES NETOYAGES SUR LE NOUVEAU CONTROLLEUR PRINCIPALE WINDOWS 2019**  

Gestionnaire DNS  
Clique-droit sur **bobdy.lan** et vérifier que dans les serveurs de noms, l'ancien serveur 2016 n'y soit plus et sinon supprimez le.  
Idem dans **bobdy.fr**   

Sites and Services Active Directory  
Supprimez le serveur WS16.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/net_AD19.png?raw=true)  

Utilisateur et ordinateurs Active Directory  
Supprimez le serveur des computers.   

Gestionnaire DNS   
Supprime le record du Windows Serveur 2019  

|***Dernière opération, dans Domaines et approbations Active Directory, clique-droit, augmenté le niveau fonctionnel de la forêt. Sur une migration AD2016 à AD2019, il n'y en a pas besoin. Par contre de AD2008 à AD2012, deAD2012 à AD2012R2 et AD2012R2 à AD2016 il y a un niveau fonctionnel à monter.***|
|:-:|

### ON VA MANIPER - MIGRATION INTER-FORET

Pour supprimer une OU: *Affichage, fonctionnalités avancées, clique-droit sur propriétés l'OU désirée, supprimer, onglet sécurité, décoché la case.*  

**Préparation de la base pour l'AD19 source et cible:**
- Désactiver les firewalls des 2 Windows Serveur.  
- Sur la carte réseau du WS19CIBLE, on fixe l'IP: 192.168.20.53  
- Renommer le nom et mettre WS19CIBLE  
- On installe les rôles Services AD DS et rôles DNS  
- Promouvoir en contrôleur de domaine complétement indépendant: **paradise.lan**  
- Faire les réglages de bases classiques  
- Mettre la réplication à 15 minutes  
- Créer son subnet dans Sites and Services AD   
- Créer son domaine commercial dans les suffixes UPN en .fr   
- On prépare les OU en prévision de la prochaine migration.  
- Même si ca communique pas encore: Mettre sur les deux cartes réseaux, les deux DNS.   

**Contrôleur Source:**

*On va créer une zone de stub*
|||
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_stub.png?raw=true)|La zone de stub va permettre de joindre la deuxième forêt.|   
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_stub2.png?raw=true)|On ajoute notre domaine cible **paradise.lan**|  
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_stub3.png?raw=true)|L'adresse IP de notre controlleur cible: 192.168.20.53|  

Vérifier que la zone est bien tombé dans les Zones de recherches directes.  

**Contrôleur Cible:**

*Dans le gestionnaire DNS, on va créer un redirecteur conditionnel.*

|||
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_redir.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_redir2.png?raw=true)|

**Contrôleur Source:**

On va faire communiquer les deux forêts et les deux domaines.  

Domaines et approbations Active Directory  
Clique-droit sur la propriété, puis Approbations  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb2.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb3.png?raw=true)   

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb4.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb5.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb6.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb7.png?raw=true)  

Si la zone d'approbation est passé c'est que la zone de stub et le redirecteur conditionnel sont bons.  

On va vérifier côté Contrôleur Cible:  
 - L'approbation est faite dans l'autre sens.   

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb8.png?raw=true)  

 - Sur le contrôleur cible, changer de domaine pour vérifier que les deux forêts communiquent.

|||
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb9.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_approb10.png?raw=true)|


**GESTION DES DROITS**

|Contrôleur Source|Contrôle Cible|
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit2.png?raw=true)|


On vas permettre une délégation de contrôle sur le domaine cible, pour rajouter le compte administrateur du domaine source au OU du domaine cible.  

|||
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit3.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit4.png?raw=true)|

*Pour afficher l'onglet sécurité, il faut faire affichage, fonctionnalité avancée.*

On rajoute l'Administrateur en contrôle total du groupe sécurité. Idem pour le groupe Staff.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit5.png?raw=true)  

On change de domaine, et on donne les mêmes droits au administrateurs sur les OU du domaine source.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit6.png?raw=true)

**Controleur Source**  

Dans l'OU Builtin, il faut créer un groupe avec le nom netbios du domaine source avec 3 fois $ : BOBDY$$$  
Il sert à ADMT(logiciel qui permet la migration) de pouvoir migrer les objets.  
Et il ne faut pas mettre de membre ! (very important)  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit7.png?raw=true)  

Ouvrir la base de registre (la crée si elle n'existe pas)
- Clé de registre:
   - [HKEY_LOCAL_MACHINE\SYSTEM\Current\ControlSet\Control\Lsa] 
   - "TcpipClientSupport"=dword:00000001  

|||
|:-:|:-:|
|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit8.png?raw=true)|![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/foret_droit9.png?raw=true)|  


**Contrôleur Source et Cible**

Gestion de Stragtégie de groupe.  
Il faut mettre une GPO en place, dans le domaine, Domain Controllers, Default Domain Controllers Policy  
Clique-droit Modifier  
Stratégie   
Paramêtre windows  
Paramêtre de sécurtié  
Stratégie Local  
Stratégie d'audit  
Auditer la gestion des comptes.  
Cocher les cases.  
![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_gpo.png?raw=true)

**Ligne de Commande**

Commande pour désactiver le SID filtering.  
 On commence par le contrôleur cible.   
> netdom trust (domaine cible) /domain:(domaine source) /quarantine:no /usero: (compte admin du controleur cible) /passwordo: (password du compte admin du controleur cible)  

donc

> netdom trust paradise.lan /domain:bobdy.lan /quarantine:no /usero:administrateur /passwordo:Dadfba16   

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_cmd.png?raw=true)

Même commande pour le contrôleur source. (évidemment on adapte la commande.)  

> netdom trust bobdy.lan /domain:paradise.lan /quarantine:no /usero:administrateur /passwordo:Dadfba16  

Commande pour activer le SID History   
On commence par le contrôleur source.   

> netdom trust (domain source) /domain:(domaine cible) /enablesidhistory:yes /usero:(compte source) /passwordo:(password source)  

donc    

> netdom trust bobdy.lan /domain:paradise.lan /enablesidhistory:yes /usero:administrateur /passwordo:Dadfba16  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/mig_cmd2.png?raw=true)  

Même commande pour le contrôleur cible. (évidemment on adapte la commande.)  

> netdom trust paradise.lan /domain:bobdy.lan /enablesidhistory:yes /usero:administrateur /passwordo:Dadfba16  

**ADMT**

Cloner un windows serveur 2016 et l'appeller ADMT  
Désactiver le pare-feu et régler la carte réseau. (192.168.20.54/24 et DNS: contrôleur cible)  
On lui donne le nom ADMT et on le met dans le domaine cible (paradise.lan)  
On redemarre.  
Et on se log en nomdedomaine\administrateur (paradise\administrateur)  

AMDT fonctionnant avec une BDD, il faut lui installer un SQL express.  
[Lien SQL Server Express](https://www.microsoft.com/fr-fr/download/details.aspx?id=55994)  
[Lien ADMT](https://www.microsoft.com/fr-fr/download/details.aspx?id=56570)  
[Lien PES](https://www.microsoft.com/en-us/download/details.aspx?id=1838)

On installe SQL express. (Déclaré en instance et serveur ADMT)  
On install ADMT (ADMT\ADMT)  
Une fois ADMT installé on peut le lancer.  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admt_install.png?raw=true)  

On va généré sa clé de chiffrement pour la donner à PASSWORD EXPORT SERVER. C'est pour que PES et ADMT puissent migrer  
Invite de commande:    
> admt key /option:create /sourcedomain:(domainesource) /keyfile:(dans le répertoire que vous voulez)\admt_key /keypassword:(mdp que vous voulez)  

> admt key /option:create /sourcedomain:paradise.lan /keyfile:c:\admt_key /keypassword:Dadfba16  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admt_prep.png?raw=true)  

On install PES sur le contrôleur de domaine source.  
Récuperer le fichier admt_key.pes crée sur le contrôleur ADMT et le mettre dans le contrôleur source pour le charger lors de l'installation.  
Prendre le compte BOBDY\administrateur (domainesource\administrateur) pour se log a PES (dans la bonne pratique, il faudrait créer un compte PES exprès)  

Maintenant, il faut vérifier plusieurs points sur le contrôleur source:
- Clé de registre:
   - [HKEY_LOCAL_MACHINE\SYSTEM\Current\ControlSet\Control\Lsa] 
   - "AllowPasswordExport"=dword:00000001  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admt_prep2.png?raw=true)

- Services.msc
  - Il faut vérifier que le service de Password Export Serveur est bien en démarré en automatique et qu'il soit démarré.

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admt_prep3.png?raw=true)

**Migration des utilisateurs**

Vérifier que le service, PASSWORD EXPORT SERVICE, soit bien démarré.  
Clique droit, assistant de migrations des comptes d'utilisateurs  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig.png?raw=true)  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig2.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig3.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig4.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig5.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig8.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig9.png?raw=true)

Une fois les utilisateurs migrés, vérifier que les utilisateurs ont bien leurs nouveaux suffixes UPN.  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig6.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig7.png?raw=true)

**Migration des groupes**

C'est identique.  

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte1.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte2.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte3.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte4.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte5.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte6.png?raw=true)

![](https://github.com/cromm24/Hello_World/blob/main/AT2/AT2C1/AD/admit_mig_compte7.png?raw=true)







**Ressources**
[AD](https://activedirectoryfaq.com/2015/10/active-directory-sid-filtering/)  

## AZURE AD CONNECT

Il s'installe sur un VM sur un AD local. Il faut le mettre sur un serveur dédié et il ne fait que ca. Il ne s'occupe que de la synchro.  
On crée un compte AD CONNECT, on le met administrateur général de MS365.

**Commande POWERSHELL**

Pour forcer la synchro:  
- Start-ADSyncSyncCycle -PolicyType Delta

Pour forcer le changement d'UPN:  
> set-MsolUserPrincipal -UserPrincipalName ancienUPN -NewUserPrincipalName nouveauUPN  

> set-MsolUserPrincipal -UserPrincipalName k.novoselic@cefim.eu -NewUserPrincipalName s.julie@cefim.eu