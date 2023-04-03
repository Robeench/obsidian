# Traditionnelle
= Standalone

Petite infra. Faible coût. Aucune sécurité si le serveur tombe. 
Maintenance importante avec un risque de panne ++

Exemple : 
VMWare ESXi
Dell EMC serveur rack ou tour

Types de stockage : 
- DAS : disque dur en attachement direct, en façade
- Stockage partagé via SAN ou NAS
- 
# Hyper-convergent
HCI = Hyper Convergent Infrastructure

avec la mise en place d'un virtual SAN (= stockage virtuel). Mise en commun du stockage physique pour plusieurs périph de stockages réseau. Impression d'un seul périph de stockage géré à partir d'une console centrale. 
En prod, nécessite une connexion de 10Gb minimum.
Nécessite du full SSD

3 nœuds minimum pour que l'infra hyperconvergée fonctionne.

## Exemple
- VMWare vSAN
- Nutanix AOS
- Datacore
