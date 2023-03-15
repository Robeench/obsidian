# Installation
## Configuration réseau
Vérifier la configuration du réseau pour permettre un accès à internet. 
IP fixe

## Rôle DNS
Gestionnaire de serveur
	Ajouter un rôle

# Gérer le service DNS
Serveur
	clic-droit
		Gestionnaire DNS

## Cache DNS
Le cache doit être à une valeur ni trop faible, ni trop forte.
Par défaut :
- 1 journée pour les réponses positives
- 15 min pour les réponses négatives

Pour afficher ces informations :
``` powershell
Get-DnsServerCache
```

![[Pasted image 20230308164102.png]]

## Interfaces
Nom du serveur 
	Propriété 
		Interfaces

Permet de définir sur quel interface mon serveur reçoit et accepte les requêtes DNS. 
Par défaut, il écoute sur toutes les interfaces, ce n'est PAS une bonne pratique. 

## Indications de racine
Serveurs racines connus de mon serveur DNS

## Tester mon serveur DNS

```shell
nslookup 10.0.0.3
www.google.com
```

## Créer ma zone inversée
Zones de recherche inversée
	Nouvelle zone

## Ajouter un enregistrement
### A ou AAAA
Zones de recherche directe
	Nom de la zone
		clic-droit
			Nouvel hôte A ou AAAA

Entrer le nom de l'hôte au sein de la zone et l'adresse IP associée

Vérification de l'enregistrement :
``` shell
nslookup intranet.nitou.lan 10.0.0.3
```
Le serveur doit me donner l'adresse IP enregistrée. 

Puis, en zone de recherche inversée.

## Transfert de zone

nitou.lan
	Propriétés
		Transferts de zone

## Autorisations pare-feu
Créer une règle entrante pour le port UDP 53