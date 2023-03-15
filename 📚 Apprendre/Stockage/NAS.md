= Network Attached Storage

Baie de stockage avec : 
- OS dédié
- logiciel de configuration
- système de fichiers
- ensemble de disques indépendants

Le NAS est rattaché au réseau de l'entreprise pour servir de [[Serveur de fichiers]]. 
Les disques durs ne sont pas reliés au serveur, mais au NAS. 
Le NAS permet l'accès client aux données, sans passer par le serveur d'application.
Il permet à plusieurs serveurs d'accéder au même fichier simultanément. 
Adapté aux applications sollicitant le système de fichiers de manière intensive. 

Echange de données entre serveur et disque en mode fichier. 
Echanges de données via les protocoles : 
- CIFS pour Windows
- SMB pour Windows
- NFS pour Unix

## Tête de NAS
système ne possédant pas de disque propre qui publie sous forme de fichiers des données blocs provenant d'un SAN. 