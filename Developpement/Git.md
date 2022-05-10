# Git
```powershell
git config --global user.name "Dynamite Jet Kid" #définit le nom d'user
git config --global user.name #indique le nom d'user en cours

git config --global user.email "benedicteleroux@tutanota.com" #définit l'e-mail
git config --global user.email #indique l'e-mail en cours

#se déplacer au sein du dossier que je souhaite transformer en dépôt Git
git init #transforme le dossier en dépôt Git
git status #permet de voir l'état de prise en compte des traquages Git
git add file1.txt #permet de traquer un fichier
git add -A #permet de traquer tous les fichiers d'un dossier
git commit #faire un backup du traquage
git commit -am "first commit" #enregistre le traquage avec le message choisi
git diff #permet de savoir les changements qui ont été importés
git log #indique l'identifiant unique de chaque commit
git log --oneline #indique chaque log sur une seule ligne
git log --graph #permet de voir de manière graphique les changements

git branch #permet de voir l'ensemble de mes branches. * montre la branche dans laquelle je me situe
git checkout -b nomDeLaBranche #crée une branche et me déplace automatiquement dedans
git branch nomDeLaBranche #crée une branche sans me déplacer dedans
git checkout nomDeLaBranche #permet de se déplacer dans la branche indiquée
git merge nomDeLaBranche #fusionne les branches
git branch -d nomDeLaBranche #supprime la branche
git branch -D nomDeLaBranche #supprime une branche non fusionnée


git push #ajouter sous GitHub
```
