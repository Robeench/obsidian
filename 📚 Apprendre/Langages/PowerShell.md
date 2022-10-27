# PowerShell

## Ecrire
``` PowerShell
write-host "Hello World !"
```


## Verbe
 `Add`  permet d’**ajouter** des données ou informations 
 `Get`  permet d’**obtenir** des données ou informations
`Read`  permet de **lire** des données ou informations
`Import` et  `Export`  permettent d’**importer**/**exporter** des fichiers de commande ou des **Alias** ;
`New`  permet de **créer** de nouveaux objets ou variables
`Set`  permet de **définir** des données ou informations
`Write`  permet d’**écrire** des données ou informations et peut agir comme le compte rendu d’une commande


## Variables
`[string]`: chaîne de caractères, on l’a déjà vu précédemment ; 
`[char]`  : caractère Unicode sur 16 bits ;
`[byte]`  : caractère sur 8 bits non signé ;
`[int]`  : valeur entière sur 32 bits signée ;
`[long]`  : valeur entière sur 64 bits signée ;  
`[bool]`  : valeur booléenne (True/False : vraie/fausse).
`[decimal]` : valeur décimale sur 128 bits
`[DateTime]` : date et heure
`[array]` : tableau de valeur

## Pipeline
`|` : la sortie d'une commande devient l'entrée de la suivante

## Fonctions
``` Powershell
PS C:\Users\benedicte.leroux> function add
>> {
>> $add =[int](2+2)
>> write-output "$add"
>> }
PS C:\Users\benedicte.leroux> add
4
```

## Commandes

`Get-Location` : savoir où je suis
`Get-ChildItem` : afficher le contenu d'un dossier
`Get-Help NomCommande -online` : m'ouvre la page complète d'aide
``Get-DnsServerCache`` : permet d'affiche le cache DNS
`-WhatIf` : m'indique ce qui se passera si j'exécute cette commande
`-confirm` : me demande la confirmation pour chaque élément