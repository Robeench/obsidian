# Microsoft 365

## [[Windows]] 365
= Win10 dans le cloud
MacOS : lancer Win365 via navigateur et cloud

## One Drive
espace de stockage cloud privé

Avantages : 
- 1To de stockage/personne
- enregistrement automatique
- versionning de fichier
- accessible partout
- possibilité de travail en déconnexion, avec synchronisation automatique ultérieure  

## Administration
### Utilisateurs 
Gestion globale des Users dans MS 365
- Azure AD
- Exchange

#### Utilisateurs actifs
UPN (User Principal Name) = identifiant unique (bleroux@cefim.eu)
		couche SSO pour un log unique.

- MS365 Apps : licence de base en dur
- Office 365 : version online
- Power Automate : analyse de données
- Contact
- Utilisateurs invités
- Utilisateurs supprimés : durée de rétention, 30 jours.

 **Pour attribuer des licenses à un groupe :**
 	création groupe d'utilisateurs
 	synchronisation AD Connect
 	attribution de la licence au groupe

### Groupes

#### Groupes actifs  
- MS 365
- Distribution : création de listes de diffusions. # fait remonter les listes des diffusions au début des contacts. 
- Sécurité : accès à des ressources ou gestion des licences (à privilégier via l'AD)  
- Groupes supprimées : 30 jours pour les restaurer
- Boite mail partagé : sans mdp  

#### Rôles  
##### Ressources
- Salles et équipement

##### Paramètres
- Domaines
- Applications 

## Azure [[Active Directory]]
- Utilisateurs : lien entre MS365 et AD
❗modification de l'UPN dans MS365, besoin d'un script [[PowerShell]] pour pousser la modification dans l'AD. Si AD vers MS365, se fait automatiquement.

- Groupes : affectation automatique de licences 
❗bloquer la création de Groupe de Sécurité et de Groupe Microsoft 365 aux users.  

- Multi-Factor Authentification : double authentification  

## Exchange
Recipient -> Mailboxes -> rechercher un user : création d'une deuxième adresse mail sans boite rattachée.

Création d'une boite mail
ajout compte utilisateur via le manage mailbox delegation, permet à chacune d'être "propriétaire"

## Teams  
AD -> Group -> General : bloquer la création de Groupe MS365 et Groupe de sécurité par l'utilisateur

- Cohabitation Teams & Skype : passer en mode Skype only - Coexistence mode le temps de la migration
Fin de la migration : passer en Teams only

Teams -> Manage Teams : création des équipes

Purger outlook
panneau de configuration -> mail -> profil -> courrier
![](https://github.com/cromm24/Hello_World/blob/AT1C4/MS365/courrier.jpg?raw=true)


### Paramétrage 
Paramètres -> Equipes et canaux -> Toutes les activités  
Equipe -> Service / Intervenant interne / Intervenant externe 

- Canaux -> Privé / Public 
- Zone de fichier : partage de fichier en temps réel  
- 1 to de stockage par équipe
	Enregistrement automatique
	Versionning de fichier
	Pas besoin de [[VPN]]
	Téléchargement de dossiers (100Go) 
	Modification en simultané  


[[PowerShell]] est indispensable !