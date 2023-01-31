# Configurations réseaux
## Bridge
Identité unique sur le réseau
L'interface réseau dispose d'une adresse IP et MAC différente de la machine hôte.
Liaison entre l'adaptateur réseau virtuel et l'adaptateur ethernet physique. 

Il est possible de configurer ce réseau pour du filaire et sans fil. 

![[Pasted image 20230131213008.png]]

## NAT
Partage les adresses IP et MAC de la machine hôte.
Périphérique NAT pour la traduction d'adresses réseaux.

Le réseau NAT fonctionne en traduisant des adresses des VM (appartenant à un réseau VMnet privée) en adresse de la machine hôte. 
Lorsqu'une VM envoie une requête pour une ressource réseau, elle est interprétée comme une demande de la machine hôte.

L'adresse de la VM est configurée via DHCP ou il est aussi possible de configurer des IP fixes, de xx.xx.xx.3 à xx.xx.xx.127. La .1 est réservée pour l'adaptateur hôte, la .2 est réservée pour le périphérique NAT. 
Le périphérique NAT fait office de gateway et server DNS par défaut. Il est possible de configurer ses VM de manière statique pour qu'elles utilisent un autre serveur DNS. 
Périphérique NAT = proxy DNS. Il transfère simplement les requêtes DNS vers un serveur DNS connu de l'hôte. 

![[Pasted image 20230131213145.png]]

## Host-Only
Le réseau ne possède qu'une existence interne, sans interconnexion avec l'extérieur. 
Adaptateur ethernet virtuel qui permet la communication entre la machine hôte et les VM.
Les adresses sont fournies par le serveur DHCP VMWare.

![[Pasted image 20230131222147.png]]

# Composants du réseau
## Switch virtuel
### VMWare
Possibilité d'en créer jusqu'à 9
Par défaut, certains commutateurs sont réservés aux configurations de base :
- vmnet0 = réseau bridge
- vmnet1 = réseau hôte uniquement
- vmnet8 = réseau NAT

## Serveur DHCP
Fournit des adresses réseaux aux VM non bridgés à un réseau externe. 
### VMWare
Les VM en réseau NAT obtiennent leurs adresses IP en envoyant des requêtes au DHCP VMWare.
Adresses de classe C : 
de xx.xx.xx.128 à xx.xx.xx.254, au sein du réseau NAT. 
Le serveur DHCP fournit aussi : la gateway, le server DNS. 

## Adaptateur réseau virtuel
Lors de la création de la VM, un adaptateur réseau virtuel est installé sur l'hôte. Il est capable d'utiliser n'importe quel type de réseau. 