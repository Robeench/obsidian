= Group Policy Object

# Définition
Ensemble d'outils intégrés à Windows Server qui permet d'automatiser la configuration des utilisateurs et ordinateurs d'une forêt.
Les paramètres s'appliquent à : 
- des postes de travail
- des serveurs
- des utilisateurs

Les GPO permettent une configuration homogène entre les différentes machines d'un parc informatique. 


Elle peut : 
- autoriser ou bloquer des paramètres
- afficher ou masquer des menus
- installer ou enlever des logiciels sur le réseau

La GPO s'applique selon une hiérarchie précise. Elle démarre de l'OU.
On peut aussi la lier au domaine entier.

Un ordinateur prendra par défaut systématiquement celle qu'il a en local. Ensuite, il prendra celle qu'il a téléchargé localement. Si une GPO n'est pas prise en compte, toujours vérifier qu'il n'y en a pas en local qui prenne le "dessus".

GPO : 
- création
- liaison
- application


