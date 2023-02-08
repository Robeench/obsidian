= Storage Area Network

## Définition
Armoire contenant plusieurs baies de disques qui sont reliées au SI par un réseau dédié, généralement via la fibre optique. 
Les disques durs ne sont pas reliés directement au serveur. Il est possible de relier un disque à plusieurs machines simultanément. 

Les baies de stockage n'apparaissent pas comme des volumes partagés sur le réseau (comme pour le NAS). Elles sont directement accessibles en mode bloc par le système de fichiers des serveurs.
Chaque serveur voit l'espace disque d'une baie SAN auquel il a accès comme son propre disque dur. 
L'espace de stockage n'est plus limité par les ressources du serveur, il est évolutif à volonté par l'ajout de disques ou baies de stockages. 
Il est plutôt utilisé pour les données applicatives. 

Pour un SAN en fibre optique, les armoires sont reliées entre elles via un switch fibre channel (= Fabric)

L'administrateur doit définir : 
- les Logical Unit Number (= numéro d'identification d'un espace de stockage)
- le masking
- le zoning
pour qu'un serveur Unix n'accède pas aux mêmes ressources qu'un serveur Windows utilisant un système de fichiers différents. 

## Avantages
- Mutualisation des ressources de stockage. 
