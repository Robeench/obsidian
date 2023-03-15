Boitier sur lequel sont présentes plusieurs prises RJ45 femelles permettant de brancher dessus des machines à l'aide de câbles à paires torsadées. 

## Table CAM
Pour envoyer la trame [[Ethernet]] vers la bonne machine, le switch se sert de l'adresse MAC. Il contient en fait une table qui fait l'association entre un [[Port]] du switch (une prise RJ45 femelle) et une adresse MAC. Cette table est appelée la table CAM. 

### Mise à jour de la table CAM
La table CAM est fabriquée de façon dynamique. Le switch va apprendre au fur et à mesure qu'il voit passer des trames, quelle machine est branchée à quel [[Port]]. 

### TTL (time to live) 
Une donnée est valable un certain temps, au delà de ce temps elle n'est plus valable. La table CAM se met donc à jour régulièrement et les données les plus anciennes sont effacées. 

### VLAN
On peut créer un réseau local virtuel (virtual [[LAN]]). C'est la capacité de séparer certains ports d'un switch. Ils ne pourront plus communiquer ensemble. Cela permet de couper le switch en plusieurs morceaux pour créer des réseaux privés. 