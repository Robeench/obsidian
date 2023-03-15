C’est un matériel de couche 3 qui relie plusieurs réseaux. Il doit donc avoir une interface pour chacun des réseaux auquel il est connecté. C’est donc une machine avec plusieurs cartes réseaux, chacune reliée à un réseau. 
Elle a pour rôle d’aiguiller les paquets reçus entre les différents réseaux.
Un ordinateur avec deux cartes réseaux pourra être un routeur. Toute machine peut jouer le rôle d’un routeur, il suffit d’activer le routage dessus (une simple machine supprimera les paquets qui ne lui sont pas destinés).

## Table de routage
Elle liste les [[Routeur]]s auxquels on peut envoyer un datagramme pour joindre une destination donnée (un réseau, pas une machine !)

On a d’un côté la liste des réseaux que l’on veut joindre, et de l’autre la liste des [[Routeur]]s à qui le datagramme doit être envoyé. Ces [[Routeur]]s sont aussi appelés des passerelles (gateway).
![table de routage](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Ftesteur-wifi.com%2Fimages%2Ftable_routage.png&f=1&nofb=1)

Si une adresse que je souhaite joindre n’appartient à aucun des réseaux indiqués dans ma table, il faudra emprunter la passerelle indiquée dans la route par défaut. 

**Comment écrire une table de routage ?**
1.  Indiquer les réseaux auxquels ma machine est connectée
2.  Indiquer la route par défaut
3.  Indiquer tous les autres réseaux que je ne peux pas encore joindre avec les deux étapes précédentes
Pour joindre un réseau, une machine doit utiliser une passerelle qui appartient à son propre réseau.