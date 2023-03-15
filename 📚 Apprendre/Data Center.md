Lieu (et un service) où sont regroupés les équipements constituants d'un [système d'information](https://fr.wikipedia.org/wiki/Syst%C3%A8me_d%27information "Système d'information") ([ordinateurs centraux](https://fr.wikipedia.org/wiki/Ordinateur_central "Ordinateur central"), [serveurs](https://fr.wikipedia.org/wiki/Serveur_informatique "Serveur informatique"), [baies de stockage](https://fr.wikipedia.org/wiki/Baie_de_stockage "Baie de stockage"), équipements réseaux et de télécommunications, etc).

## Environnement contrôlé
climatisation, poussières, alimentation

## Environnement sécurisé
système anti-incendie, contre le vol et l'intrusion ...

# Redondance
Alimentation d'urgence et redondante
redondante = les services de base et les systèmes auront des doublons (équipement, liaisons, alimentation et chemins, données, logiciels…)

Haute disponibilité = obtenue par la redondance, au niveau de tout l'écosystème

![[Introred.jpg]]

## Uptim Institute
Consortium d'entreprise créé en 1993, qui a pour but de maximiser l'efficacité des data center.
A défini la notion de TIER.

### TIER
Système de classification. Les data center doivent être certifiés par l'Uptime Institute pour revendiquer un niveau de Tier. C'est le seul organisme à délivrer des certifications, même si d'autres organismes proposent des classifications. 
Chaque niveau reprend les caractéristiques précédentes.

![[Pasted image 20230202211231.png]]
![[Pasted image 20230202211244.png]]

#### Tier I - Basique
Site basique, sans redondance. 
- [ ] salles informatiques dédiées
- [ ] onduleur
- [ ] système de refroidissement dédié
- [ ] groupe électrogène disposant d'une réserve de carburant permettant le fonctionnement pendant 12h
- [ ] un arrêt annuel pour maintenance

#### Tier II - Redondance de la production d'électricité et du refroidissement
- [ ] redondance des "Infrastructure Capacity Components" (= production électrique, protection électrique, refroidissement) SAUF les circuits de distribution
- [ ] un arrêt manuel pour maintenance
Infrastructure Capacity Components = générateurs électriques, stockage du carburant, stockage d'énergie, onduleurs, groupes froids, climatisations, protections calorifuges. 

#### Tier III - Maintenabilité
Maintenabilité sans arrêt de l'informatique.
- [ ] tous les composants et circuits de distribution sont redondants
- [ ] les groupes électrogènes doivent pouvoir fonctionner à charge nominale (N) sans limitation de durée. Cela implique que les valeurs de groupe à retenir est la « Continuous Power » (CP) selon la norme ISO8528.1. Un déclassement de 30 % de la PRP (Prime Rating Power) est à appliquer aux groupes ne déposant de classification « CP ».
- [ ] aucune maintenance ne doit provoquer un arrêt de l'informatique
- [ ] certaines pannes, incidents ou erreurs humaines peuvent interrompre l'informatique

#### Tier IV - Tolérance aux pannes
- [ ] tous les composants et distributions sont maintenables sans impact informatique
- [ ] réponse automatique aux pannes uniques
- [ ] compartimentage coupe-feu
- [ ] continuous cooling : assurer le refroidissement en absence totale d'alimentation électrique
- [ ] groupe électrogène fonctionnant sans limitation de durée
- [ ] absence de single point of failure (SPOF)
- [ ] tolérance aux maintenances, pannes (uniques) et incidents même graves (incendie...)


# Disaster Recovery
un ou plusieurs sites de sauvegardes
besoin de planification efficace et solutions validées : Quel process ? 

# Récupération à la suite d'une défaillance
## Echec en réseau
multi-homing = plusieurs fournisseurs d'accès à internet ??

## Echec d'un dispositif
mise en place de cluster

## Redondance de passerelle par défaut
protocole de redondance de [[Routeur]]

