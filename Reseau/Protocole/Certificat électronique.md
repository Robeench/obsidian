[[Protocole]], [[SSL - TLS]], [[HTTPS]]
# Certificat électronique
Ensemble de données contenant : 
- une clé publique
- des informations d'identifications
- une signature

Il est infalsifiable, nominatif et certifié. 
La certification est payante. 

Les certificats électroniques respectent des standards qui spécifient leur contenu de manière rigoureuse : 
- [X.509](https://fr.wikipedia.org/wiki/X.509) via la [RFC 5280](https://datatracker.ietf.org/doc/html/rfc5280) : ne peut contenir qu'un seul identifiant qui contient de nombreux champs prédéfinis et ne peut être signé que par une seule autorité de certification. 
- [OpenPGP](https://fr.wikipedia.org/wiki/OpenPGP) via le [RFC 4880](https://www.rfc-editor.org/rfc/rfc4880) : peut contenir plusieurs identifiants, avec une certaine souplesse dans le contenu et peuvent être signés par une multitude d'autres certificats.
