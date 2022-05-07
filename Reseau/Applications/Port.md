[[Applications]], [[IP]], [[Protocole]]
# Port
Lors de l'envoi de paquets, l'adresse IP permet de retrouver uniquement le serveur hébergeant mais pas l'application concernée. 
Chaque application a un numéro de ports attribuée. 

La combinaison adresse IP + n° de port est appelée SOCKET. C'est une adresse unique. 
Les données sont alors envoyées au bon endroit.

Il existe 65 535 ports.

### Ports reconnus
Ports 0 à 1023.
Réservés pour les processus systèmes. 
Numéro de port fixe associés à des services réseaux spécifiques configurés par les administrateurs réseaux.

### Ports enregistrés
Ports 1024 à 49151.
Ports attribués pour un service spécifique, sur demande, par une organisation.

### Ports dynamiques et / ou privés
Ports 49 152 à 65 535.
Utilisés pour l'allocation dynamique de ports éphèmères valables pour la durée d'une connexion. Ou pour des services privés ou personnalisés.