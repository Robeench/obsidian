But = se mettre d'accord sur ce qu'on veut, ce qui peut être fait, combien ça coûte.

- Le serveur applicatif décrit dans ce document correspond aux outils connexes plugués à l'ERP ?
Tout est sur le même serveur, plugué au sens de l'ERP.
Les plugins sont intégrés à Odoo via des modules. Les fichiers connexes sont via l'API

- Quels sont les fournisseurs / hébergeurs de la solution ?
Get Caas = nouvel acteur (environ 2 ans d'ancienneté)
https://getcaas.io/

- Schéma de l'architecture serveur ?
architecture technique = François
architecture applicative = Pierre-Vincent
documentation des API = disponible via le code source

- Si on passe à plus de 1000 membres que se passe-t-il pour le serveur mutualisé ? Est-ce qu'on migre ? y a-t-il un coût ?
le serveur est surdimensionné, donc il pourra supporter plus de 1000 membres. Pas de limites.
Les serveurs sont scalables si besoin de plus de processeur ou RAM, il y a des paliers qui permettent de voir venir l'évolution si besoin.

- Quelle est la sécurité mise en œuvre (tentatives d'intrusion => comment est ce détecté ?)
Un point d'entrée global
Réseau interne pas adressable depuis l'extérieur
Pas d'information en +, Pierre-Vincent se renseigne
Réplication en temps réel
Sauvegarde à froid de base, tous les jours pendant 15 jours.

- Redondance ou planning des MAJ et MEP ?
On est prévenu par Coopératic des MAJ applicatives, elles se font en dehors des heures d'ouvertures. Pas le vendredi. Du mardi au jeudi. Idéalement le mercredi.
Les montées de version font partie des heures cumulées de "support"
On a la possibilité de leur annoncer en amont nos périodes de fermeture, notamment au début du lancement du supermarché.
MAJ de l'OS (linux) géré par GetCaas. Nous avons un accès SSH au serveur de dev et pré-prod

- Est-ce Coopératic qui gère les snapshots des serveurs sur tout environnement confondu ?
Les sauvegardes journalières et leurs gestions se font par GetCaast
L'installation des images est faite par François.

- pourquoi 24 par an ? pourquoi ce chiffre ?
24 appels par an pour éviter les abus.
Limite jamais atteinte dans les autres coopératives.

- plateforme de suivi des interventions => pourrait-on avoir un accès pour voir l'outil de ticketing en avance de phase ?
outil redmine
pas d'accès en amont du contrat possible

- SAV le samedi ?
Non
Les caisses sont dans tous les cas toujours disponibles.
Avoir un routeur 4G de secours via Bouygues.
les caisses ont besoin d'internet au lancement et à la fermeture. Entre les deux c'est uniquement du local.
Toujours fermer la caisse le soir, puis la réouvrir le soir même. Permet que tout soit ok le matin avant qu'ils commencent à intervenir (9h)
Problème possible : Odoo tombe et ne redémarre pas. Ca n'est jamais arrivé.
A part la caisse + le TPE, tout est possible par papier en solution de contournement si problème.
Le serveur qui porte tout l'applicatif est redondé en direct

- Qu'est ce qu'on entend par 'Espace membre' ? Il y a quoi derrière ce module (Pas vu de vidéo sur ce sujet dans Cooperatic_Tube) ?
à revoir mercredi 26.10

- Quel sera le support de formation ? aurons nous accès à une instance Odoo avec toutes applis connexes ?
Pas de support de formation.
Incitation à créer notre propre wiki.

- Pour chaque module et l'ERP, à combien estimez-vous le temps d'apprentissage ?
Pas de possibilité de l'estimer. Très différent selon les équipes, le temps que l'on passe entre les sessions à tester, etc ...

- Dans le cas de la formation distancielle, quel sera l'outil de visio ? Peut-on enregistrer les sessions ?
BigBlueButton ou Zoom
Autorisation d'enregistrement ok

- Quelles sont les horaires et jours de formation sur la semaine ?
lundi au vendredi de 9h à 18h
plus cher sinon
sur les 2 jours en présentiel, besoin du maximum de l'équipe projet.
Graou Coop - Julien Guillaume

- Est-ce que le tarif est dégressif quand on augmente le nombre de jour ou est ce linéaire ?
tarif dégressif à 120€ de l'heure

- En cas de retard sur la résolution d'incident y a-t-il des pénalités ?
fonctionnement en temps d'intervention, pas d'astreinte.
la résolution dépend de l'incident. S'ils passent plus d'une heure au diagnostic, ils nous avertissent et on définit ensemble le temps de travail alloué sur ce problème.
ils ne vendent pas un logiciel mais du temps pour l'installer et le maintenir. Donc ils allouent des heures de travail sur ce logiciel, tout ce qui dépasse doit être financé par nos soins.
Nous payons le temps pour chaque ticket.

- Y-a-t-il une mutualisation des problèmes/incidents ?
Oui

- Est ce que les 2h démarre à la prise en compte ou à l'ouverture du ticket ?
à la création du ticket

- Contrat
période de garantie d'un mois
forfait à l'heure
solde au moment du passage de la pré-prod à la prod
on choisit le démarrage du contrat TMA
On paie l'hébergement quand on lance la commande

- où met on les utilisateurs ?
Dans Odoo, mais ils peuvent être ailleurs. Le plus simple c'est Odoo.
Notre base utilise YouKnowHost
Dans Odoo c'est des comptes génériques, rares sont les personnes qui ont des comptes personnels.


# Conclusion
On retire le volet SSO et on valide ce contrat. 
Pour le SSO, un avenant au contrat d'installation sera possible dans un second temps.