
# Ethernet

[Format des trames Ethernet](https://repository.root-me.org/R%C3%A9seau/FR%20-%20Format%20des%20trames%20Ethernet.pdf)
[Les réseaux Ethernet : le format des trames](https://repository.root-me.org/R%C3%A9seau/FR%20-%20Les%20r%C3%A9seaux%20Ethernet%20-%20le%20format%20des%20trames.pdf)


L'objectif des réseaux est de pouvoir s'échanger des informations. L'échange se fait entre des machines différentes, avec des OS différents (MacOS, [[Linux]], [[Windows]] ...) et il existe donc un langage commun de communication pour se comprendre : le Protocole Ethernet. 

## Trame 802.3
![[Pasted image 20220930211153.png]]
- Adresse MAC destination - 6 octets
- Adresse MAC source - 6 octets
- Longueur des données - 2 octets
- Données à envoyer - 46 à 1500 octets
- FCS - 4 octets : valeur mathématique représentative des données envoyées qui permet de repérer les erreurs de transmission. 

L'en-tête de la trame Ethernet est de 18 octets. Sa taille minimale est de 64 octets, et la taille maximale de 1518 octets. 

## Trame ethernet II
![[Pasted image 20220930211259.png]]
La différence entre Ethernet II et 802.3 se fait au niveau du 3ème champ :
802.3 < 1500
Ethernet II > 1500

### Valeurs du champ protocole
![[Pasted image 20220930211452.png]]
