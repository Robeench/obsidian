La virtualisation de serveurs est un ensemble de techniques et d’outils permettant de faire tourner plusieurs systèmes d’exploitation sur un même serveur physique. Le principe de la virtualisation est donc un principe de partage : les différents systèmes d’exploitation se partagent les ressources du serveur.

L'hyperviseur contrôle le processeur. 
Les principaux éléments physiques utilisés sont le [[CPU]], la [[Carte graphique]], la mémoire [[RAM]], l'espace du disque dur ... 

# Principes fondamentaux
## Cloisonnement
Chaque système d’exploitation a un fonctionnement indépendant, et ne peut interférer avec les autres en aucune manière

## Transparence
Le fait de fonctionner en mode virtualisé ne change rien au fonctionnement du système d’exploitation et a fortiori des applications.

# Avantages
- baisse du nombre de serveurs physiques
- disponibilité performante
- performances accrues
- sécurité optimale
- solution anti-obsolescence
- économie sur les licences
- facilité dans les sauvegardes
- gestion plus simple du [[Plan de Reprise d'Activité]]
- essayer sans surcoût
- avenir tourné vers le cloud

# Inconvénients
- augmentation de la criticité de la machine en cas de panne matérielle
- sécurité des accès
- accès aux VM à partir du système hôte
- suivi des performances et du service
- indisponibilité des serveurs
- ouverture de l'espace de stockage des VM
- prise de contrôle du système par l'hôte

# Configurations réseaux
## Bridge
Identité unique sur le réseau
L'interface réseau dispose d'une adresse [[IP]] et MAC différente de la machine hôte.
Liaison entre l'adaptateur réseau virtuel et l'adaptateur [[ethernet]] physique. 

Il est possible de configurer ce réseau pour du filaire et sans fil. 

![[Pasted image 20230131213008.png]]

## NAT
Partage les adresses [[IP]] et MAC de la machine hôte.
Périphérique NAT pour la traduction d'adresses réseaux.

Le réseau NAT fonctionne en traduisant des adresses des VM (appartenant à un réseau VMnet privée) en adresse de la machine hôte. 
Lorsqu'une VM envoie une requête pour une ressource réseau, elle est interprétée comme une demande de la machine hôte.

L'adresse de la VM est configurée via [[DHCP]] ou il est aussi possible de configurer des [[IP]] fixes, de xx.xx.xx.3 à xx.xx.xx.127. La .1 est réservée pour l'adaptateur hôte, la .2 est réservée pour le périphérique NAT. 
Le périphérique NAT fait office de gateway et server [[DNS]] par défaut. Il est possible de configurer ses VM de manière statique pour qu'elles utilisent un autre serveur [[DNS]]. 
Périphérique NAT = [[proxy]] [[DNS]]. Il transfère simplement les requêtes [[DNS]] vers un serveur [[DNS]] connu de l'hôte. 

![[Pasted image 20230131213145.png]]

## Host-Only
Le réseau ne possède qu'une existence interne, sans interconnexion avec l'extérieur. 
Adaptateur [[ethernet]] virtuel qui permet la communication entre la machine hôte et les VM.
Les adresses sont fournies par le serveur [[DHCP]] VMWare.

![[Pasted image 20230131222147.png]]

# Composants du réseau
## [[Switch]] virtuel
### VMWare
Possibilité d'en créer jusqu'à 9
Par défaut, certains commutateurs sont réservés aux configurations de base :
- vmnet0 = réseau bridge
- vmnet1 = réseau hôte uniquement
- vmnet8 = réseau NAT

## Serveur [[DHCP]]
Fournit des adresses réseaux aux VM non bridgés à un réseau externe. 
### VMWare
Les VM en réseau NAT obtiennent leurs adresses [[IP]] en envoyant des requêtes au [[DHCP]] VMWare.
Adresses de classe C : 
de xx.xx.xx.128 à xx.xx.xx.254, au sein du réseau NAT. 
Le serveur [[DHCP]] fournit aussi : la gateway, le server [[DNS]]. 

## Adaptateur réseau virtuel
Lors de la création de la VM, un adaptateur réseau virtuel est installé sur l'hôte. Il est capable d'utiliser n'importe quel type de réseau. 