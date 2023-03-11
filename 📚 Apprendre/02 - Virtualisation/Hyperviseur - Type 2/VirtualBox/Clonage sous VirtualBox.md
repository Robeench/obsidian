# Configuration

Lors du clonage, l'identifiant unique (SID) de Windows reste le même.
Pour éviter tout conflit, il faut regénérer un nouvel identifiant unique : 
``` shell
cd C:\Windows\System32\Sysprep
sysprep
# Ouverture de l'application "Outil de préparation système"
```

🗂 Entrer en mode OOBE
	Généraliser
		Arrêter le système ou Redémarrer
			Ok

Suite au redémarrage, la configuration initiale de Windows va se lancer comme au premier démarrage, cela permettra la réinitialisation du SID. 
Pour autant, les données ne seront pas supprimées et les applications seront conservées.

# Ressources
[IT-Connect - Comment cloner une machine virtuelle](https://www.it-connect.fr/comment-cloner-une-vm-virtualbox/#III_Mefiance_lorsquune_machine_est_clonee)
