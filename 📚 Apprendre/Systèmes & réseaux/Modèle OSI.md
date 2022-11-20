
# Modèle OSI
Ce modèle est créé en 1984. C'est une norme préconisant la manière dont les machines communiquent entre elles. C'est un modèle théorique. Le modèle réel utilisé est le [[Modèle TCP IP]].
C'est un modèle en 7 couches. Chaque couche est indépendante, cela garantit qu'elles sont interchangeables. Chaque couche communique uniquement avec celles qui lui sont adjacentes. 

![Modèle OSI](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2F2.bp.blogspot.com%2F-Y2konI8y35Y%2FWZBVKHYBbAI%2FAAAAAAAAB1k%2FUL4tCHJGPGobKTzonrSRTJmQxQLezRcEACPcBGAYYCw%2Fs1600%2FOSI.png&f=1&nofb=1)

## Couche 1 - Physique
Offre un support de transmission pour la communication. Connexion physique sur le réseau pour l'émission et la réception des bits.
Matériel : Hub, [[Switch]], [[Routeur]]

Elle permet d'acheminer les signaux électriques (0 et 1) via différents supports de transmission.
### Câbles
#### Câble coaxiaux
![Câble coaxial](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fuser.oc-static.com%2Ffiles%2F258001_259000%2F258382.gif&f=1&nofb=1)

Le signal électrique circule dans le fil de données. Le maillage de masse permet d'avoir un signal de référence à 0V et on obtient le signal électrique en faisant la différence entre le fil de données et le maillage de masse. 

##### Câble coaxial 10B5
Il fallait faire un trou dans le câble pour atteindre le fil de données. Ensuite une prise vampire (avec une pointe en métal) permettait d’être en contact avec le fil et de récupérer le signal. S’ils étaient pliés, le réseau était coupé et le fil bon à jeter, sans possibilité d’en remplacer une seule partie.

##### Câble coaxial 10B2
C’est plus simple et plus solide que le 10B5 car si un câble est défectueux on peut le remplacer mais si qq’un se débranche du réseau, il coupe tout le réseau.

#### Paire torsadée 10BT
Il n’y a plus un fil unique mais huit, torsadés deux à deux par paires. Dans le principe, il n’y a besoin que de deux fils pour faire passer la différence de potentiel. Il a été créé avec 8 fils pour permettre son évolution. Aujourd’hui, on utilise souvent 4 fils : une paire pour envoyer les données, une paire pour recevoir.
Lorsque l’on pose du câble, il faut éviter de le poser à côté de câbles à 220V ou des néons qui créent de grosses perturbations.
Nom scientifique : 10BT ou 100BT ou 1000BT selon le débit utilisé.
T = torsadé
On branche les machines dessus à l’aide de la prise RJ45 : 
![RJ45 mâle](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmedia.hubo.be%2Fimg%2FCable-ethernet-RJ45-20m_904383_000_1920x1440.jpg%3Fbase%3Dimages%26sub%3Dhb0%26bottom%3Dh2c%26name%3D9139693977630.jpg%26context%3DbWFzdGVyfGltYWdlc3wxMTI1NjV8aW1hZ2UvanBlZ3xpbWFnZXMvaGIwL2gyYy85MTM5NjkzOTc3NjMwLmpwZ3w1ZTY2OWIzN2JmZDViMWVmNDZiNGM0ZTg0ZjIzMTJjNDNmMzI0Y2JhYzYzZTgwZWU4ZGRmNzlmYzFhMjAwNTcz%26attachment%3Dtrue&f=1&nofb=1)

![RJ45 femelle](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.leroymerlin.fr%2Fmultimedia%2F5a1400199913%2Fproduits%2Fadaptateur-rj45-categorie-5-femelle-femelle-evology.jpg&f=1&nofb=1)
[[Switch]] : 
![Switch](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Feu.dlink.com%2Ffr%2Ffr%2F-%2Fmedia%2Fproduct-pages%2Fdgs%2F105%2Fdgs105b1image-lfront.png&f=1&nofb=1)
Lorsqu’il y a plusieurs machines connectées au hub, s’il reçoit une information il l’envoie à toutes les machines.

#### Fibre optique
Le transport des 1 et 0 se fait avec de la lumière. Elle est utilisée chez les opérateurs internets qui nécessitent beaucoup de bande passante, dans les grandes entreprises, dans certaines entreprises où il y a trop de perturbations électromagnétiques (vu que la lumière y est insensible)

##### Fibre monomode
Elle fait passer une seule longueur d’onde lumineuse soit une seule couleur. Fonctionne avec du laser. Plus performante que la multimode car la couleur ne peut pas s’éparpiller.
Distance parcourue : environ 60km
##### Fibre multimode
Elle fonctionne avec de la lumière blanche, donc toutes les longueurs d’ondes (lumière blanche = somme de toutes les couleurs possibles)
Distance parcourue : environ 2km

### Topologie réseau
Manière de brancher les machines entre elles. Il existe trois typologies principales. 

##### En bus
Toutes les machines sont branchées sur le même câble. Une seule machine peut parler à la fois car il y a un seul câble. On considère qu’au-delà de 50 machines, le réseau ne marche plus. La taille du réseau doit être limitée pour limiter le risque que plusieurs machines parlent en même temps.

##### En anneau
N’existe plus.
Un « jeton » tourne en permanence sur l’anneau et les machines peuvent le prendre pour envoyer un message. Pas de possibilités d’une infinité de machine car un seul jeton pour tous. La taille du réseau doit aussi être limitée.

##### En étoile
Toutes les machines sont branchées à une machine centrale (comme un [[Switch]]) qui sait envoyer les informations à une machine en particulier.
Toutes les communications passent par le point central. On envoie l’information et le point central aiguille vers la bonne machine. Plus le [[Switch]] peut traiter un grand nombre de machines, plus on peut brancher de machines. Aujourd’hui, les switches peuvent traiter plusieurs milliers de machines. On peut faire un réseau de taille illimitée en reliant plusieurs switches entre eux, ainsi ils peuvent transmettre l’information jusqu’au destinataire.

### CSMA / CD
Carrier Sense Multiple Access / Collision Detection
Dans une typologie en bus, deux machines ne peuvent pas parler en même temps, sinon il se produit une collision. On peut essayer de limiter ces collisions en instaurant cette règle :
- On écoute en permanence sur le bus pour savoir si qq’un parle
- On ne peut parler que quand il est libre
- Si jamais on parle, qu’une collision survient, on se tait et on attend (un temps aléatoire) pour reparler

## Couche 2 - Liaison de données
Son rôle est de connecter des machines sur un réseau local. L’objectif est de permettre à des machines connectées ensemble de communiquer. Elle permet aussi de détecter les erreurs de transmission (détecter pas corriger !).
Matériel : [[Switch]], [[Routeur]]
Protocoles : [[Ethernet]], PPP (point to point protocol)

### Adresse MAC
C'est l'adresse de ma carte réseau, écrite en hexadécimal. Chaque carte réseau a sa propre adresse MAC, unique, et elle est codée sur 6 octets, soit 48 bits. L’adresse ff:ff:ff:ff:ff:ff est l’adresse de broadcast. C’est une adresse universelle qui identifie n’importe quelle carte réseau.

#### Calcul binaire
Tout nombre décimal s'écrit comme une somme de puissance de 2. 
[IP calculator](http://jodies.de/ipcalc)
[[[IP]] calcul masque de sous réseaux](http://vlsmcalc.net/)

#### Calcul hexadécimal
On utilise les chiffres de 0 à 9 et les lettres de A à F. 

## Couche 3 - Réseau
Assure le routage des paquets entre les noeuds du réseau. 
Matériel : [[Routeur]]
Protocole : [[IP]]
### Appréhendez la notion de réseau
#### [[LAN]]
[[LAN]] = Local Area Network
réseau à l'échelle locale, tels qu'un réseau domestique ou à l'échelle d'une entreprise.

#### [[MAN]]
[[MAN]] = Metropolitan Area Network
déployés à l'échelle d'une ville. Par exemple un réseau universitaire qui connectent différentes facultés d'une même ville. Ils sont constitués de [[LAN]] qui ensemble, forment un [[MAN]].

#### [[WAN]]
[[WAN]] = Wide Area Network
Réseau à l'échelle mondiale, dont le plus connu est internet. Il est composé de [[MAN]] et de [[LAN]].

### Distinguez schéma logique et schéma physique
Le schéma logique permet de concevoir, modéliser et configurer mon réseau.
Le schéma physique permet de déployer le réseau, installer et cabler le matériel. Il apporte des informations complémentaires :
-   localisation physique des équipements
-   nombre de cables utilisés pour relier les éléments
-   nombre exact de machines sur le réseau
-   vue plus détaillée des équipements d'interconnexion

## Couche 4 - Transport
Gère les connexions applicatives et fragmente les paquets. Elle choisit la meilleure façon d'envoyer une information. 
Protocole : UDP, TCP

## Couche 5 - Session
Gère l'organisation des échanges en établissant, maintenant et terminant les sessions d'échange. 
Non utilisé

## Couche 6 - Présentation
Elle encode, compresse, convertit et reformate les données.
Non utilisé

## Couche 7 - Application
Point d'accès pour l'utilisateur aux services applicatifs
Matériel : [[Proxy]]
Protocole : SMTP, [[HTTP]], FTP ...
