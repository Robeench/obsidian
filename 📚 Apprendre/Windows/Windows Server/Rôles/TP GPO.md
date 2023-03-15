# Interdire les jeux intégrés de Windows

# Interdire le Shell (sans l'exécution des scripts) sur une OU 
[IT-Connect - Comment bloquer PowerShell pour les utilisateurs](https://www.it-connect.fr/comment-bloquer-powershell-pour-les-utilisateurs/)

🗂 Configuration utilisateur
	Stratégies
		Paramètres Windows
			Paramètres de sécurité
				Stratégies de restriction logicielle
					Règles supplémentaires
						Nouvelle règle de chemin d'accès
							Bloquer les accès pour PowerShell x32, x64 et PowerShell ISE
								chemin d'accès = C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe
								C:\\Windows\\sysWOW64\\WindowsPowerShell\\v1.0\\powershell.exe
								C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell_ise.exe
								C:\\Windows\\sysWOW64\\WindowsPowerShell\\v1.0\\powershell_ise.exe
								niveau de sécurité = non autorisé

Cette GPO est possible via la configuration machine ou utilisateur.

# Lancer un script VBS sur une OU au démarrage
[Developpez - FAQ VBScript](https://vb.developpez.com/faq/vbs/)
[Wikimedia - VBScript](https://commons.wikimedia.org/wiki/Category:VBScript?uselang=fr)

Définition de scripts d'ouverture de session, qui exécute des commandes dès l'ouverture de la session. Il peut s'agir de :
- mappage d'un lecteur réseau
- installation ou configuration de l'imprimante par défaut
- collecte d'informations
- mise à jour des signatures de l'antivirus
- mise à jour du système
- ...

## Création du script
Créer script sous bloc-notes, enregistrer dans le format souhaité :
- Script Visual Basic (.vbs)
- Batch de commandes Windows (.bat)
- Script de commandes Windows (.cmd)

``` sql
Dim Shell, DesktopPath, URL 
  
Set Shell = CreateObject("WScript.Shell") 
DesktopPath = Shell.SpecialFolders("Desktop") 
Set URL = Shell.CreateShortcut(DesktopPath & "\MonForumPreferé.URL") 
URL.TargetPath = "http://www.developpez.net/forums" 
URL.WorkingDirectory = "c:\tmp" 
URL.Save
```

Enregistrer sous :
	%SystemRoot%\\SYSVOL\\Sysvol\\nitou.lan\\Scripts


🗂 Configuration ordinateur
	Stratégie
		Paramètres Windows
			Scripts
				Démarrage
					Ajouter

# Lancer un script VBS "utile" sur une OU au log off


## Changer le papier peint des usagers par celui de votre entreprise et le bloquer
🗂 Configuration utilisateur
	Stratégies
		Modèles d'administration
			Bureau
				Bureau
					Papier peint du bureau

- Activé la GPO
- Nom du papier peint = \\srv-ad-tou-01\\common\\wallpaper.jpg
- Déplacer la GPO sur l'OU = TOURS

- [ ] Supprimer des éléments du panneau de configuration

- [ ] Charger les ADMX pour firefox

- [ ] Charger les ADMX pour office 2010/2013

## Charger les ADMX pour Edge
🗂 Configuration utilisateur
	Stratégies
		Modèles d'administration
			❗❗ Il n'y a pas de composants pour Edge ❗❗

Je peux ajouter des composants via : 
🗂 Ce PC
	C:
		Windows
			PolicyDefinitions
Récupérer le fichier de modèle d'administration au format ADMX via le [site de Microsoft](https://www.microsoft.com/en-us/edge/business/download?form=MA13FJ)
Ouvrir le fichier MicrosoftEdgePolicyTemplates
	Windows
		Copier les 3 fichiers ADMX + le fichier de langue sous PolicyDefinitions
Je peux désormais accéder au composant Edge. 

- [ ] Charger les ADMX pour Chrome
- [ ] Modifier le navigateur IE de tous vos client pour qu'il affiche "powered by votre entreprise" dans la barre de titre


- [ ] Modifier le navigateur IE de tous vos client pour qu'il affiche comme page par défaut www.cefim.eu

- [ ] Modifier le navigateur Firefox de tous vos client pour qu'il affiche powered by votre entreprise dans la barre de titre

- [ ] Modifier le navigateur Firefox de tous vos client pour qu'il affiche comme page par défaut www.cefim.eu

- [ ] Modifier le navigateur Chrome de tous vos client pour qu'il affiche powered by votre entreprise dans la barre de titre


- [ ] Modifier le navigateur Chrome de tous vos client pour qu'il affiche comme page par défaut [https://www.votredomaine.tld](https://www.votredomaine.tld)


- [ ] Créer des GPO corporate pour office (modèle de document, police par défaut, auteur)

- [ ] Interdire une application portable par hashage du binaire

- [ ] Mapper un lecteur réseau via un .bat

- [ ] Mapper un lecteur réseau via la console GPO

- [ ] Mettre un écran de veille au bout d'une minute avec verrouillage

- [ ] Interdire l'usage d'une clé USB

- [ ] Déployer une application via MSI

- [ ] Créer une redirection de dossier

- [ ] Créer une GPO pour activer le pare-feu des clients

- [ ] Créer une règle dans le firewall des clients pour forcer le ping

# Problèmes
https://www.it-connect.fr/les-gpo-ne-sappliquent-pas-14-pistes-a-etudier/
