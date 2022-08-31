
# Firewall
Element du réseau informatique étant logiciel et/ou matériel. 
Il définit les connexions autorisées ou interdites. 
Il permet de connecter deux réseaux ou plus avec des niveaux de sécurité différente. Il contrôle les flux de données en entrée et sortie et rejette si besoin certaines données. 

## Règles de filtrage
- Origine ou destination des paquets
- Options contenues dans les données
- Données
- Utilisateurs

## Types de firewall
### Stateless Packet Inspection Firewall
Pare-feu sans état
Il regarde chaque paquet indépendamment les uns des autres et le compare à une liste de filtrage appelée Access Control List (ACL).

Il accorde ou refuse le passage de paquets en se basant sur : 
- [[IP]] source / destination
- [[Port]] source / destination
Tout échange avec des ports non autorisés sera bloqué. 

Limites : L'admin va devoir autoriser un trop grand nombre d'accès 

### Stateful Packet Inspection Firewall
Pare-feu à états
Il vérifie que chaque paquet d'une connexion est la suite du précédent paquet et la réponse à un paquet dans l'autre sens. 
Si une connexion est autorisée, tous les paquets de l'échange seront implicitement acceptés. 

Il maintient un tableau des états (= connexions ouvertes) avec les connexions autorisées existantes. 

### Firewall Applicatif
Filtrage applicatif, c'est à dire en fonction de chaque application.
Les requêtes sont traités par des procédures dédiées. Il vérifie que le paquet correspond au [[protocole]] attendu. Il rejette donc toutes les requêtes n'y correspondant pas.

Il joue aussi le rôle de [[Proxy applicatif]].

### Pare-feu identifiants
Firewall capable de réaliser l'identification des connexions à travers le filtre [[IP]]. 
L'admin peut donc définir les règles de filtrage par utilisateurs, et non plus par adresse [[IP]] ou adresse MAC.

### DeMilitarized Zone (DMZ)
Le firewall permet de créer un sous-réseau séparé et isolé du réseau local et d'internet. Il est appelé [[DMZ]]. 
Il contient les machines susceptibles d'être accessibles via internet : serveur de messagerie, serveur web ...
Le sous-réseau bloque l'accès au réseau local pour garantir sa sécurité.

![[Capture d’écran 2022-05-04 093747.png]]

### Firewall personnel
Fonctionne uniquement sur une machine, au lieu de protéger un réseau.