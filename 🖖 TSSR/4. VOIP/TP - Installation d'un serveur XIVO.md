# Généralités
Une communication c'est 64kb/s de consommation de bande passante . 
Une infrastructures dans laquelle on place de la VOIP doit avoir : QOS + VLAN + POE  
* QOS : prioriser un trafic minimum de la voix quand le reste est surchargé selon la règle 
64kbps x NbDeLigneSimultanée
* VLAN : isoler le trafic VOIP dans un réseau spécifique
* POE (ou POE+) :alimenter les IP Phones

# Installation
Création d'une VM avec 2Go de [[RAM]] minimal, sur un noyau linux, branche Debian10 x 64bits 
avec l'[iso XIVO](http://mirror.xivo.solutions/iso/xivo-current/) current la plus récente (❗bien faire attention à être dans le bon dossier current, et pas dans le directory, sinon la version de Xivo ne fonctionne pas)

Nous installerons par la suite deux softphones :
- un sur le Win10 hôte
- un sur un smartphone Android/IOS

Je me connecte à mon serveur XIVO depuis un poste client avec l'adresse http://192.168.X.X/, correspondant à l'adresse IP de mon serveur. 
Warning potentiel du navigateur, je force la connexion. 
* Choix de la langue française
* Validation de la licence GNU-GPL 
* Nom de l'hôte : SRVXIVO 
* Domaine : nitou.lan 
* Password  
* Adresse IP : 192.168.X.X (eth0), à mettre de préférence en IP fixe
* Gateway : 192.168.X.X (celle fournie par ma box) 
* DNS : 192.168.1.254  (celle fournie par ma box), dans une vrai infra je renseigne ici le [[Serveur DNS]] local qui est souvent le DC1 de l'AD
* Entité : nom de mon entreprise
* Nom affiché : Appels internes  
* Début de l'intervalle des numéro : 100  
* Fin de l'intervalle : 199  

[XIVO - Présentation et installation](https://www.networklab.fr/xivo-presentation-et-installation/)

# Configuration du serveur

Configurer mon serveur : [XIVO - Guide utilisateur](https://assistance.ac-noumea.nc/IMG/pdf/xivo_guide_utilisateur.pdf)
Menu IPBX

## Gestion
Définir un contexte d'entreprise dans entités :
* ligne téléphonique extérieur
* e-mail de la société
* adresse url de la société
* adresse
* ville
* CP

**Général** : laisser coché, permet de relancer les services automatiques après une modification.
**Certificats SSL** : pas besoin car la connexion est déjà sécurisée même si elle est auto-signée, dans une infra locale complète on monte une PKI mais ici je n'en ai pas besoin.
**Serveurs LDAP** : Permet d'importer les users d'un AD. 

## Contexte d'approvisionnement
IP phone : besoin de les approvisionner
Softphone : pas besoin

**Modèles de terminaison** : si on rajoute un appareil, il se base sur ce template. Mettre le protocole en SIP.
**Greffons** : ajout du pack xivo-cisco-spa-7.5.5 

❗un softphone n'a pas besoin de greffons. 

## Services IPBX 
**Protocole SIP** : on lui fait confiance, je n'ai rien à changer ! 
**Messageries vocales** : les fréquences 8khz donne un son de mauvaise qualité, possibilité de changer les sonneries. 
**Terminaison:**  terminaison physique, nécessaire si on a des IP Phones.

Pour qu'un softphone sonne, il me faut juste un utilisateur et un ligne attribué. 
L'attribution des lignes sur utilisateurs ou inversement. Les deux sont interdépendants. 

**Lignes** :
* Associer à l'utilisateur un identifiant et un mot de passe (XIVO les génèrent automatiquement)  
* Création de 2 lignes : Bénédicte Le Roux et Maxime Fayaud

**Utilisateurs** :    
* Ajouter un compte : Bénédicte Le Roux
* Ajouter un compte : Maxime Fayaud

# Configuration softphone

## Poste hôte - Win10 - Jitsi

[Téléchargement du softphone Jitsi](https://desktop.jitsi.org/Main/Download.html)
[Configuration softphone](https://xivopourlesnuls.wordpress.com/2014/04/19/configuration-des-softphones/)

Fichier
	Ajouter un nouveau compte
		réseau : SIP
		nom d'utilisateur : identifiant à récupérer dans la ligne concernée, sur le serveur XIVO
		mot de passe : à récupérer dans la ligne concernée, sur le serveur XIVO
	Cliquer sur Avancé
		renseigner le nom à affiché
		registrar : saisir l'adresse IP du serveur

J'essaye de m'appeler, tout est ok. 

## Poste client - Android - Zoiper

[Télécharger Zoiper](https://www.zoiper.com/en/voip-softphone/download/current)
[Configuration Zoiper](https://docs.web2contact.com/pages/docs/fr/parametrages/utiliser-zoiper.html)

