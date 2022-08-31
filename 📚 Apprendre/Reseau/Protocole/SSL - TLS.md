[[Protocole]]
# Secure Sockets Layer (SSL) - Transport Layer Security (TLS)

[[Protocole]] de sécurisation des échanges sur internet. 
SSL est obsolète, on utilise désormais TLS

Le chiffrement consiste à transformer les données en les rendant illisibles via un algorithme de chiffrement et une clé de chiffrement. 
La clé de chiffrement est une suite de bit qui sert à chiffrer et déchiffrer les données. C'est l'équivalent d'un mot de passe. 
L'algorithme de chiffrement est une méthode de chiffrement. 

[Vidéo - Comprendre le chiffrement](https://www.youtube.com/watch?v=7W7WPMX7arI&t=216s)


## Cryptographie symétrique
Pour échanger des données, Alice et Bob ont une même clé secrète. Pour envoyer un message qui sera uniquement lu par Bob, Alice le chiffre avec sa clé secrète, l'envoie à Bob et Bob le déchiffre avec la clé secrète. Pour répondre de manière sécurisée, Bob peut le faire de la même manière. 
Il y a une seule clé pour chiffrer et déchiffrer un message.
**Inconvénients** : l'échange des clés doit se faire sur un canal sécurisé.
**Avantages** : peu gourmand en ressource [[Processeur - CPU]]


## Cryptographie asymétrique
On utilise deux clés : la clé privée et la clé publique. 
Quand l'utilisateur chiffre avec la première clé, il peut déchiffrer avec la deuxième clé. Et inversement. Ces deux clés sont liées mathématiquement.
La clé privée n'est JAMAIS transmise à personne. 
On diffuse la clé publique. 
Le chiffrement se fait avec la clé publique, et seule la personne avec la clé privée liée peut déchiffrer le message.
**Inconvénients** : demande de grosses ressources [[Processeur - CPU]]


On passe ensuite de la cryptographie asymétrique à la cryptographie symétrique car l'asymétrique est trop gourmand en ressources. La cryptographie asymétrique permet d'échanger la clé privée puis, utilisation de la cryptographie symétrique pour la rapidité du chiffrement.
