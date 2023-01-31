
# IPv4
La version 4 reste la plus utilisée malgré la pénurie d'adresses. 
IPv6 doit la remplacer.

Notation décimale avec 4 valeurs comprises entre 0 et 255, séparées par des points. Sa longueur est de 32 bits soit 4 octets.

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

