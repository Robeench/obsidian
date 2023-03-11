# Installation
## Gestion du stockage
Eteindre le serveur

 🗂 Machine
	Settings
		Storage
			Création d'un nouveau contrôleur USB
				Ajout de deux nouveaux disques

🗂 Redémarrer mon serveur
Services de fichier et de stockage 
	Disques
		Clic droit sur chaque disque
			Initialiser

🗂 Créer un pool de stockage
Sélectionner le pool de stockage
	Nouveau disque dur virtuel

## Partage

🗂 Partages
	Ressources partagées
		Nouveau partage

### Dossiers de travail
[Microsoft - Déploiement de dossiers de travail](https://learn.microsoft.com/fr-fr/windows-server/storage/work-folders/deploy-work-folders)
Mise en place d'un dossier personnel synchronisé avec un serveur de fichier en HTTPS.
A mettre en place uniquement si pas de OneDrive/Sharepoint en entreprise. 

#### Emplacement des dossiers de travail
Sur le serveur où j'installe la fonctionnalité, je crée un dossier qui va recevoir les dossiers utilisateurs. 

#### Enregistrement DNS
Créer un enregistrement DNS "workfolder.nitou.lan" qui pointe sur le serveur. 

#### Fonctionnalité dossier de travail
🗂 Ajouter des rôles et des fonctionnalités
	Rôle service de fichier et de stockage
		Dossiers de travail

🗂 Services de fichiers et de stockage
	Dossier de travail
		Nouveau partage de synchronisation
			Entrer le chemin du dossier HOME
			Format du nom de dossier : alias utilisateur
			

### Quotas

[Microsoft - Gestion des quotas](https://learn.microsoft.com/fr-fr/windows-server/storage/fsrm/quota-management)
Peuvent être créés à partir d'un modèle ou avec des propriétés personnalisés. 

#### Modèle
Permet de gérer les quotas de manière centralisée. 
- quota unique qui limite l'espace pour l'intégralité d'un volume
- quota d'application automatique

Accéder au quota d'un dossier : 
🗂 Services de fichiers et de partage
	Partages
		Quota

#### Quota automatique
Affectation d'un modèle de quota qu'on peut affecter à un volume ou dossier parent. 

🗂 Dossier de travail
	Quota
		Gérer les modèles de quota

