# Installation

[Installation et configuration du rôle AD-DS](https://vadmintic.wordpress.com/systemes-windows/installation-et-configuration/installation-et-configuration-du-role-ad-ds/)

## Configuration
- Renommer le serveur

## Configuration réseau
Adressage réseau fixe, avec les deux serveurs dans le même réseau. 
Pour vérifier la connectivité, désactiver temporairement le pare-feu. 

## Contrôleur de domaine
🗂 Serveur
	AD DS
		Promouvoir ce serveur en contrôleur de domaine
			Ajouter une nouvelle forêt et définir le domaine racine (nitou.lan) 
			Choisir le niveau fonctionnel de la forêt et du domaine (niveau le plus bas de mes serveurs)
	Reboot

Mon domaine est configuré et actif.

# Outils d'administration

## Centre d'administration Active Directory
Centralise toutes les possibilités d'administration courante
Plus d'informations sur la documentation [Microsoft](https://learn.microsoft.com/fr-fr/windows-server/identity/ad-ds/get-started/adac/active-directory-administrative-center)

🗂 Outils d'administration
	Centre d'administration Active Directory

## Utilisateurs et ordinateurs Active Directory
Représentation graphique de l'annuaire

🗂 Outils d'administration
	Utilisateurs et ordinateurs Active Directory
		Nom de domaine
			Nouveau
				Unité d'organisation

# Groupes
## Groupe de domaine local
GDL = Groupe de Domaine Local
Contenant uniquement des membres de mon domaine local.

## Groupes globaux
GG = Groupes Globaux
Si j'ai plusieurs domaines dans ma forêt et que je souhaite que les membres des différents domaines puissent accéder aux mêmes ressources. 

## Groupes universels
GU = Groupes Universels
Lorsque mes ressources peuvent être issues de tous les domaines au sein d’une forêt. Autorise des membres issus de n’importe quel domaine d’une forêt.

## Nomenclature type
GG_R_IMPRIMANTE_RDC = groupe global restreint pour l'imprimante du rez de chaussée.
GU_U_Accès-Internet = groupe universel d'utilisateurs ayant accès à internet.

# GPO
## Paramètres d'une GPO
### Utilisateur
En fonction de l'utilisateur connecté, quelque soit la machine.

### Machine
En fonction de la machine, quelque soit l'utilisateur connecté.

### Stratégies
#### Paramètres logiciels
Gérer les déploiements logiciels de façon centralisée.
❗ L'installeur du logiciel doit être au format MSI. 

#### Paramètres Windows
Regroupent les différents scripts qu'il est possible d'écrire pour exécuter des actions à des moments clés : démarrage du poste, connexion d'un utilisateur ...
Certains paramètres sont dispo uniquement pour l'utilisateur (internet explorer) ou la machine (pare-feu).

#### Modèles d'administration
fichiers au format ADMX permettant de gérer la base de registre Windows. 

#### Préférences
Simplification de nombreuses tâches avec une interface graphique proche de ce qui est disponible sur un poste client. 

## Vérifier l'application de la GPO

``` shell
# Afficher l'application des GPO
gpresult /R

# Application des paramètres GPO
gpupdate /force
```
