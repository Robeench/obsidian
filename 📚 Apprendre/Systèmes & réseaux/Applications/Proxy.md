
# Proxy
Serveur intermédiaire qui permet à une application ou un internaute d'accéder à internet. 

Il permet : 
- le filtrage des accès à des sites internet ;
- de contourner les filtrages (il masque les données personnelles techniques (adresse [[IP]], OS, détails techniques du navigateur, [traces numériques](https://fr.wikipedia.org/wiki/Trace_num%C3%A9rique) ...) à tous les sites visités. Vu que les données entre le client et le service anonymiseur sont chiffrées, le fournisseur d’accès peut difficilement connaitre les sites visités. Mais, le service anonymiseur y a obligatoirement accès !) ;
- une accélération de la navigation (via la compression des données, le filtrage des contenus, la fonction de cache) ;
- suivi de connexions via les logs (enregistre l'ensemble des requêtes)

## Reverse Proxy
Permet à un utilisateur d'internet d'accéder à des serveurs internes. 
Il protège les serveurs web internes des attaques provenant de l'extérieur.

Il permet : 
- de porter le chiffrement SSL ;
- d'accélérer la navigation ;
- répartition de charges des requêtes externes vers les serveurs en interne. 

