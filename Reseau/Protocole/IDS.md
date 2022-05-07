[[Protocole]]
# Intrusion Detection System (IDS)
Repérer tout type de trafic pouvant être malveillant.
Il détecte les activités s'éloignant de la norme (et produit une alerte si besoin) et surveille les activités d'une cible (réeau, machine hôte ...).

## Network IDS
Surveille l'état de la sécurité du réseau. 
Il voit une copie du trafic.
En cas de détection de menaces il peut créer des alertes et ordonner les actions pour le blocage d'un flux. 

Il se situe sur un réseau isolé
Il ne voit qu'une copie du trafic de réseau à surveiller
Il ne communique pas avec le réseau surveillé

## Host IDS
Surveille l'état de sécurité des hôtes via :
- nombre et listes de processus
- nombre d'utilisateurs
- ressources consommées

Surveille les activités de l'utilisateur via : 
- horaires et durée de connexion
- commandes utilisées
- programmes activés

Il récupère les informations remontées par les machines hôtes, analyse ces informations, puis surveille l'état de sécurité. 