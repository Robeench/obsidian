
# IPv4
La version 4 reste la plus utilisée, la version 6 devrait la remplacer.
Notation décimale avec 4 valeurs comprises entre 0 et 255, séparées par des points. Sa longueur est de 32 bits soit 4 octets.
Exemple : 192.168.1.10

## Les classes
La notion de classe d'adresse [[IP]] a été utilisé pour distribuer des plages d'adresses à des utilisateurs finaux. Elle est désormais obsolète, on utilise les masques de sous réseaux.
Il y a 5 classes différentes : A, B, C, D, E.
[Classe d'adresse IP - Wikipédia](https://fr.wikipedia.org/wiki/Classe_d%27adresse_IP)

### Adresses [[IP]] privées et publiques
#### Privées
On peut les utiliser pour un équipement sur un réseau local. Elle ne peut pas être utilisée sur internet, car elles ne sont pas routées sur internet.
Classe A = 10.0.0.0 à 10.255.255.255
Classe B = 172.16.0.0 à 172.31.255.255
Classe C = 192.168.1.0 à 192.168.255.255

Le choix d'une adresse s'effectue en fonction des besoins et du nombre d'équipements à connecter en simultané sur ce réseau.

#### Publiques
Elles sont utilisées exclusivement sur internet. Elle est unique dans le monde.
Classe A = tout sauf de 10.0.0.0 à 10.255.255.255
Classe B = tout sauf de 172.16.0.0 à 172.31.255.255
Classe C = tout sauf de 192.168.1.0 à 192.168.255.255

### Exceptions
Le réseau 127.0.0.0 est réservé pour la boucle locale, défini par défaut sur chaque machine.
Le réseau 0.0.0.0 est réservé pour définir une route par défaut sur un [[Routeur]].

## Masque de sous-réseaux
[IP Calculator](http://jodies.de/ipcalc)
[Calculateur IP sous-réseau, CIDR](https://ceipam.eu/fr/ipcalculator.php)

Les bits à 1 dans le masque représentent la partie réseau. Les bits à 0 représentent la partie machine.

Première adresse du réseau : tous les bits de la partie machine sont à 0 - adresse du réseau, ne peut pas être utilisé pour une machine.
Dernière adresse du réseau : tous les bits de la partie machine sont à 1 - adresse de broadcast, permet d'identifier toutes les machines de mon réseau. Quand un message est envoyé à cette adresse, il est envoyé à toutes les machines de ce réseau. 

Nombre d’adresses dans un réseau : 2 puissance nombrede0danslemasque

#### Exemple entre 2 octets
Adresse [[IP]]
192.168.0.1 > **11000000.10101000**.00000000.00000001
Masque de sous réseau
255.255.0.0 > **11111111.11111111**.0000000.0000000

#### Exemple au milieu d'1 octet
Adresse [[IP]]
192.168.0.1 > **11000000.10101000.0000**0000.00000001
Masque de sous réseaux
255.255.240.0 > **1111111.11111111.1111**0000.00000000
On ne peut pas repasser en décimal lorsque la coupure a lieu au milieu d'un octet. On ne peut pas écrire une partie d'un octet, on peut donc uniquement s'exprimer en binaire. 

On retrouve toujours les mêmes valeurs pour les octets d'un masque : 
00000000 -> 0
10000000 -> 128
11000000 -> 192
11100000 -> 224
11110000 -> 240
11111000 -> 248
11111100 -> 252
11111110 -> 254
11111111 -> 255