
# Switch
Boitier sur lequel sont présentes plusieurs prises RJ45 femelles permettant de brancher dessus des machines à l'aide de câbles à paires torsadées. 

![Switch](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5fe1d5dc-486b-4d6a-bdf8-dbb79b1c051d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220224T165403Z&X-Amz-Expires=86400&X-Amz-Signature=e04111540116d8a8d7ed49abb3e1bca0c54e1fd7f8fd1557f974998700ae1d8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

## Table CAM
Pour envoyer la trame [[Ethernet]] vers la bonne machine, le switch se sert de l'adresse MAC. Il contient en fait une table qui fait l'association entre un [[port]] du switch (une prise RJ45 femelle) et une adresse MAC. Cette table est appelée la table CAM. 

Par exemple, pour cette image : 
![Exemple switch](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/004351ff-8fed-4249-aa97-d4a59e3183d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220224%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220224T165903Z&X-Amz-Expires=86400&X-Amz-Signature=1aec08761e216f2e87475a5f467d24cf3bd447c9821567922d66fe396e9c0c3f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
La table CAM sera : 
[[Port]] | @MAC
 --- | ---
1 | @MAC 23
2 | @MAC 24
3 | @MAC 25

Quand la machine 23 veut envoyer une trame à la machine 25, le switch lit l'adresse de destination et saura vers quel [[port]] envoyer la trame. 

###  Mise à jour de la table CAM
 La table CAM est fabriquée de façon dynamique. Le switch va apprendre au fur et à mesure qu'il voit passer des trames, quelle machine est branchée à quel [[port]]. 

 ### TTL (time to live) 
 Une donnée est valable un certain temps, au delà de ce temps elle n'est plus valable. La table CAM se met donc à jour régulièrement et les données les plus anciennes sont effacées. 

 ### VLAN
 On peut créer un réseau local virtuel (virtual [[lan]]). C'est la capacité de séparer certains ports d'un switch. Ils ne pourront plus communiquer ensemble. Cela permet de couper le switch en plusieurs morceaux pour créer des réseaux privés. 