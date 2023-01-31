
# Active directory
# Cours
C'est un service d'annuaire [[LDAP]] pour les OS [[Windows]] utilisé pour stocker des informations relatives aux ressources réseau sur un domaine. 
C'est une organisation hiérarchisée d'objets classée en 3 catégories : 
- ressources (imprimantes, ordinateurs ...)
- services (courrier électronique ...)
- utilisateurs (compte utilisateur, groupes ...)

## Contrôleur de domaine et domaine
### Modèle groupe de travail
Les postes [[Windows]] sont par défaut dans un groupe de travail "WORKGROUP".
La base d'utilisateurs est locale, appelée base SAM.
Inadapté lorsque le nombre de postes et d'utilisateurs augmente car lourd en administration.
Simple à mettre en oeuvre pour le partage de fichiers entre quelques machines. 

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
Utilisation des protocoles [[LDAP]], [[DNS]] et [[Kerberos]].

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

