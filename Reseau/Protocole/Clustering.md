
# Clustering
Désigne un groupe de serveurs vu de l'extérieur comme un seul et même serveur.
Il permet de traiter des applications auquels un seul serveur ne pourrait pas faire face. Et il permet une haute disponibilité des apllications.
La redondance des serveurs garantit la haute disponibilité des services et prémunit des pannes.

## Cluster actif / passif
Doublé un serveur avec un deuxième serveur similaire. Les deux serveurs sont démarrés mais un seul traite les requêtes.
Il répond à un besoin de disponibilités, pas a un besoin de montée en charge. 

## Cluster actif / actif
On redonde le serveur actif avec d'autres serveurs similaires. La charge de travail est répartie entre tous les serveurs. 
Il permet de gérer la montée en charge et permet une meilleure disponibilité. 
Par contre il faut gérer des problèmes de concurrence entre bases de données et des sessions utilisateurs pour les serveurs d'applications.

### Répartition de charge statique
On peut répartir la charge en fonction de différents critères : 
- localisation géographique
- type d'utilisateurs
- ...

### Répartition de charge dynamique
Matériel : load balancer (= répartiteur de charge)

Algorithmes utilisés pour la répartition de charges : 
- Round robin
- Round robin pondéré
- Least connection

## Pannes
### Fail over
Transfert d'un processus d'un serveur à un autre

### Fail back
Réintégrer dans un cluster un serveur qui a subi une défaillance. 
Permet d'éviter de redémarrer l'intégralité du cluster.


