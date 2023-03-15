# Installation

🗂 Ajouter un rôle ou une fonctionnalité
	Serveur DHCP

Notification : 
	cliquer sur Terminer la configuration

🗂 DHCP
	clic droit
		Gestionnaire DHCP

# Gérer le serveur
## Stopper, démarrer, redémarrer
🗂 Nom du serveur DHCP
	Clic-droit
		Toutes les tâches

## Base de données
🗂 Nom du serveur DHCP
	Clic-droit
		Propriétés

## Etendues
Plage d'adresses IP assignées aux ordinateurs demandant une adresse IP dynamique. 

🗂 IPv4
	clic-droit
		Nouvelle étendue

## Autoriser les flux DHCP
🗂 Outils d'administration
	Pare-feu Windows avec fonctions avancées de sécurité
		Créer une Règle de trafic entrant
			UDP - Ports 67 et 68

## Configurer un basculement
🗂 IPv4
	clic-droit
		Configurer un basculement

# Problèmes

Vérifier :
- la disponibilité des baux
- si deux offres de configuration identiques ont été distribués ?
- mes flux DHCP sont-ils ouverts ? 
- mon serveur est-il joignable sur le réseau ?
- le journal d'événements
