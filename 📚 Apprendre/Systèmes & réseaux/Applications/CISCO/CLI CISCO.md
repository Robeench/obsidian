= Command Line Interface

Interface en ligne de commandes de CISCO, divisée en hiérarchie CISCO : 

![[1626813031839_schéma.png]]

## Mode utilisateur
= User EXEC command
Mode de commande pour afficher des renseignements sur le matériel. 

Pour passer en mode privilège : 
```
enable
```

## Mode privilège
= Privileged EXEC command
Equivalent à root en linux. 
utilisateur + gestion des fichiers à l'intérieur du routeur

Pour passer en mode configuration globale :
```
configure terminal
```

## Mode configuration globale
= Global Configuration command
sous-mode du mode privilège. 
permet la configuration du routeur.

``` shell
interface FastEthernet 0/1 #permet la connexion au mode configuration d'interfaces
```

### Mode configuration d'interfaces
= Interface command
configurer les adresses, masques, etc. 

### Mode configuration du routage

### Mode configuration de ligne

