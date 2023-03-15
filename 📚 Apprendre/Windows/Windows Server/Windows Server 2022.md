# Editions

## Essentials
Pour les petites entreprises et organisations jusqu'à 25 utilisateurs et 50 équipements. 
❗ Pas possible de mettre à jour vers Standard

## Standard
Pour les entités n'ayant pas de forts besoins de [[Virtualisation]] ou à faible densité (peu de serveurs).
Pas de limitation de machines virtuelles mais il faudra acquérir des licences supplémentaires. 
La tarification est basée sur le nombre de cœurs sur le serveur physique. 

## Datacenter
Haut de gamme.
Possibilité de créer autant de machines virtuelles que je le souhaite. 
Tarification basée sur le nombre de cœurs des serveurs physiques.
Nécessite une licence d'accès client pour chaque machine cliente. 

# Installation - [[Windows]] Server Standard

## ISO
[Récupérer l'ISO de [[Windows]] Server](https://info.microsoft.com/ww-landing-windows-server-2022.html?lcid=fr)

## Configuration minimale requise
[Microsoft - Configuration matérielle requise pour Windows Server](https://learn.microsoft.com/fr-fr/windows-server/get-started/hardware-requirements)

- 1 [[CPU]]
- 2Go de [[RAM]]
- 32Go de disque SSD

## Connexion réseau
Définir le type de connexion réseau

## Mises à jour
Vérifier et lancer si besoin les mises à jour via [[Windows]] Update.

## Nommage
Nommer mon serveur, avec une nomenclature cohérente, type : 
SRV1-ADDHCPDNS

## Configuration réseau
Toujours vérifier et fixer la configuration réseau :
 - adresse [[IP]]
 - masque
 - passerelle
 - [[Serveur DNS]]
Si l'[[IPv6]] n'est pas utilisé sur mon réseau, la désactiver. 

## Pare-feu
Rechercher "Defender"
	Modifier les paramètres de connexion
		Bloquer toutes les connexions et m'avertir en réseau privé et public

## Rôles, fonctionnalités et services

![[Pasted image 20230308132703.png]]

### Rôles
-   Accès à distance ;
-   Attestation d’intégrité de l’appareil ;
-   Hyper-V ;
-   Serveur de télécopie ;
-   [[Serveur DHCP]] ;
-   [[Serveur DNS]] ;
-   Serveur Web (IIS) ;
-   Service Guardian hôte ;
-   Services [[AD]] DS ;
-   Services [[AD]] LDS ;
-   Services [[AD]] RMS ;
-   Services Bureau à distance ;
-   Services d’activation en volume ;
-   Services d’impression et de numérisation de documents ;
-   Services de certificats Active Directory ;
-   Services de déploiement [[Windows]] ;
-   Services de fédération Active Directory ([[AD]] FS) ;
-   Service de fichiers et de [[stockage]] ;
-   Service de stratégie et d’accès réseau ;
-   Service WSUS ([[Windows]] Server Update Services).

## Surveillance
### Tableau de bord
### Serveur local
Permet de retrouver les configurations de base de mon serveur :
- réseau, nom, état des mises à jour ...
- événements des différents journaux d'événements du serveur

#### Evénements
Par défaut, les événements critique, erreur et avertissement sont affichés. 

#### Services
Etat de tous les services du serveur. Je peux relancer, arrêter ou démarrer un service directement ici. 

#### Best Practice Analyzer
Permet de vérifier la conformité aux bonnes pratiques Microsoft. 

#### Performance
Outil pour diagnostiquer un problème de ressources sur le serveur. 
Tâches > Configurer des alertes de performance
	Clic-droit sur le nom du serveur
		Démarrer les compteurs de performance

#### Rôles et fonctionnalités
Récapitulatif des rôles et fonctionnalités
