
# Modèle TCP / IP
## Couche 1 - Accès au réseau
Correspond aux couches Liaison et Physique du [[Modèle OSI]].
Protocole : Adresses MAC
Matériels : Câbles [[Ethernet]], fibres, wifi, bluetooth

## Couche 2 - Internet
Correspond à la couche Réseau du [[Modèle OSI]].
Protocole : [[IP]]

## Couche 3 - Transport
Correspond à la couche Transport du [[Modèle OSI]].
Protocole : TCP, UDP

## Couche 4 - Application
Correspond aux couches Application, Présentation et Session du [[Modèle OSI]].
Protocole : [[DHCP]], [[DNS]], FTP, [[HTTP]], [[SSH]], SMTP...


## Encapsulation
En émission, les données traversent chacune des couches, et à chacune des couches une information est ajoutée au paquet de données, il s'agit d'une en-tête. L'en-tête définit le protocole utilisé à chaque couche. 
Ensuite à la réception, l'en-tête est lue, interprétée, puis supprimée. A la réception au niveau de l'application, la donnée arrive dans son état initial. C'est la désencapsulation.

## Protocol Data Unit
En passant par chaque couche le paquet change d'aspect.
Le PDU permet d'identifier un message en fonction de sa position dans le modèle TCP / IP.
Couche 1 = Trame
Couche 2 = Datagramme
Couche 3 = Segment
Couche 4 = Message
Couche physique = Bits

