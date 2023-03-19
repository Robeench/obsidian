
Nettoyage automatique de disque : https://www.proservices-informatique.fr/nettoyage-automatique-disque-windows-10/

https://www.it-connect.fr/windows-10-comment-supprimer-les-anciens-profils-utilisateurs/



``` shell
cd /d c:\  
cd "Documents and Settings"  
dir /ad /b> syst.txt  
set path1=Default User  
set path2=All Users  
set path3=LocalService  
set path4=NetworkService  
for /f "tokens=*" %%G IN (syst.txt) DO (  
if "%%G" == "%path1%" echo stop> stop.txt  
if "%%G" == "%path2%" echo stop> stop.txt  
if %%G == %USERNAME% echo stop> stop.txt  
if %%G == %path3% echo stop> stop.txt  
if %%G == %path4% echo stop> stop.txt  
if not exist stop.txt rmdir /s /Q "%%G"  
if exist stop.txt del stop.txt  
)  
if exist syst.txt del syst.txt  
del c:\windows\prefetch\*.* /q  
rem exit
```

A enregistrer en .bat

Le script commence par remplir un fichier syst.txt avec le listing des dossiers contenu dans le  
dossier « Documents and Settings ».  
Ensuite, il remplie des variables avec le nom des quatres dossiers qu'il ne faut surtout pas  
supprimer (Default User, All Users, LocalService et NetworkService).  
Puis il lance une boucle qui va comparé la valeur de chaque ligne du fichier texte avec les  
condition suivantes :  
Est ce que le nom du fichier est égale à Variable 1 ou Variable 2 ou %Username% ou  
Variable 3 ou Variable 4.  
Si un des cas est valide, le fichier stop.txt est créer à la racine de « Documents and Settings ».  
Dernier test, si le fichier stop.txt n'existe pas alors le dossiers est supprimer sinon si le fichier  
stop.txt existe, le fichier stop.txt est supprimer et la boucle recommence jusqu'à la fin du  
listing.  
Une fois que la liste est finit, le fichier syst.txt et supprimer.  
La suppression des fichiers du dossier Prefetch permet de gagner en rapidité d'execution sur  
les système Microsoft.