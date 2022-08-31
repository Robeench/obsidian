[[Protocole]]
# Ethernet
L'objectif des réseaux est de pouvoir s'échanger des informations. L'échange se fait entre des machines différentes, avec des OS différents ([[MacOS]], [[Linux]], [[Windows]] ...) et il existe donc un langage commun de communication pour se comprendre : le [[protocole]] Ethernet. 

Chaque message est envoyé sous la trame : 
- Adresse MAC destinataire - 6 octets
- Adresse MAC source - 6 octets
- [[Protocole]] de couche 3 ([[Modèle OSI]]) - 2 octets
- Données à envoyer
- CRC - 4 octets : valeur mathématique représentative des données envoyées qui permet de repérer les erreurs de transmission. 
L'en-tête de la trame Ethernet est de 18 octets. Sa taille minimale est de 64 octets, et la taille maximale de 1518 octets. 
