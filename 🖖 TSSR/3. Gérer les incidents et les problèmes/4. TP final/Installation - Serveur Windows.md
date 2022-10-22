## IV. Montage d'un Windows Serveur 2019 et mise en lien avec GLPI <a name="III"></a>

* Au moins un domaine controler, mono domaine, mono serveur.  <br/>
* tld : top level domain ( comme . fr; 1er niveau)  <br/>
* FSMO : Flexible Single Master Operation, certains types de contrôleurs de domaine dans Active Directory, de Microsoft. Ce sont ceux qui jouent un rôle nécessitant un maître unique pour la réplication entre contrôleurs de domaine ; certains rôles sont uniques pour tous les domaines de la forêt ; d’autres rôles sont plus simplement uniques à l’intérieur d’un domaine. <br/>
* AD DS : active directory domain service <br/>
* Le niveau fonctionnel de la foret : windowsSer 2019 n'est pas un vrai OS, c'est plus le nom marketing de win ser 16 version 2 donc pas de news, on est sur une base de 2016. 2019 c'est plus une maj.  


<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>

- [Qu'est-ce qu'un DNS via WIkipedia](https://fr.wikipedia.org/wiki/Domain_Name_System)<br/>
- [Le DNS via le site frameip](https://www.frameip.com/dns/)<br/>
- [Controller de domaine et domaine via it-connect](https://www.it-connect.fr/chapitres/controleur-de-domaine-et-domaine/)<br/>
- [Rôle de l'herbergement de domaine et DNS via Wikipedia](https://fr.wikipedia.org/wiki/H%C3%A9bergement_de_nom_de_domaine)<br/>
- [Explication des 5 rôles FSMO via le site it-connect](https://www.it-connect.fr/chapitres/les-cinq-roles-fsmo/) <br/>
- [Infos Wikipedia sur les TLD](https://fr.wikipedia.org/wiki/Domaine_de_premier_niveau)<br/>
- [Lignes de commandes CMD usuelles](https://www.ionos.fr/digitalguide/serveur/know-how/commande-cmd/)<br/>

</details>


L'idée sera de créer un WServer qui servira de server entre notre GLPI et les usagers via un AD. Pour commencer il faudra donc monter un WServer propre et ensuite paramétrer l'AD pour gérer notre server GLPI. PLus précisément nous allons monter une machine Serveur qui doit s'occuper des noms de Second niveau ; et à un AD correspond non un serveur mais un nom de domaine au moins. Le premier contrôleur de domaine que nous installerons dans la forêt jouera les cinq rôles de la FSMO.  

### A) Préparation d'une baseline WServeur 2019 <a name="IIIA"></a>

* Install de 7zip, Notepad++, SumatraPDF, Chrome via Ninite
* Pare feu en privé avec règle ICMP
* Workgroup : TSSR
* Hostname : DC1
* IP FIXE en IPv4
* IPv6 désactivée sur la carte ethernet0
* Configuration de sécurité renforcée désactivée pour IE
* Bureau à distance activé
* Mise à jour désactivée 
* Suppression des MAJ via sconfig
* Clonage du master réalisé pour le futur

Toutes ces manips sont dispo via le *cmd* en tapant :
-> `sconfig` 
-> (1) Groupe de travail, (2) Nom de l'ordi, (4+7) Admin à distance, (5) MAJ, (8) Paramètres réseaux

Possible de passer par *Ninite* pour installer les softs.
> `appwiz.cpl` dans CMD pour vérifier les softs

![Check des softs installés](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/appwiz.jpg.png)

Infos paramètres réseau
-> `ncpa.cpl`

![ncpa](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/ncpa.png)

### B) INstallation d'un AD <a name="IIIB"></a>

<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>

* [Mise en place d'un environnement AD](https://rdr-it.com/mise-en-place-environnement-active-directory/)<br/>
* [Définition d'un AD via wikipedia](https://fr.wikipedia.org/wiki/Active_Directory)<br/>
* [Monter un AD sur WServer2019 via technet365.fr](https://technet365.fr/installation-active-directory-sur-windows-serveur-2019/)<br/>
* [Installation d'un AD via techexpert.tips](https://techexpert.tips/fr/windows-fr/installation-dactive-directory-sur-windows-server/)<br/>
* [Administration simplifiée d'un AD via la doc Microsoft](https://docs.microsoft.com/fr-fr/windows-server/identity/ad-ds/manage/ad-ds-simplified-administration)<br/>

</details>


Une machine Serveur qui doit s'occuper des noms de Second niveau ; et à un AD correspond non un serveur mais un nom de domaine au moins

#### --- Installation de l'AD --- <a name="IIIB1"></a>

Sur la console *« Gestionnaire de serveur »*, nous allons ajouter le rôle AD DS.

- Ajouter un rôle et des fonctionnalités
- Services AD / DS

Une fois l’installation terminée, depuis la console *« Gestionnaire de serveur »* nous allons promouvoir le serveur en contrôleur de domaine

- **Nouvelle forêt** : **tssr.lan**
- Dans Option du contrôleur de déploiement, rentrer un nouveau mot de passe : Admin7007 (**générique : dadfba16**)
- Pas de gestion DNS

![Forêt tssr.lan](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/for%C3%AAt%20tssr.lan.png)

![AD](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/AD.jpg)

#### --- Ajout d'un OU --- <a name="IIIB2"></a>

- Outil
- Utilisateur et Ordinateur
- Création d'un dossier **Usagers** à la racine *tssr.lan* (nouvel OU/UA)

![Nouvel OU Usagers](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/Nouvel%20OU.png)

#### --- Génération d'une base d'users --- <a name="IIIB3"></a>

1. On va passer par [Generatedata.com](https://www.generatedata.com/) afin de randomniser des noms pour enusuite réaliser un export csv<br/>
- 4 colonnes : prénom, nom, mdp (pin)<br/>
    -> générer en csv

2. Ensuite on passe par **excel** afin de modifier le CSV afin de le compléter :<br/>
* <span style="color: #32977E">=MINUSCULE(STXT(A8;1;1))&""&MINUSCULE(B8)</span> : création d'un login *1e lettre prenom+nom*<br/>
ou <span style="color: #32977E">=MINUSCULE(CONCATENER(STXT(A3;1;1);B3))</span><br/>
* <span style="color: #32977E">=MINUSCULE(CONCATENER(STXT(A3;1;1);B3;"@tssr.lan"))</span> : création d'un email <br/>
* <span style="color: #32977E">=("02"&ALEA.ENTRE.BORNES(10000000;99999999))</span> : création d'un n°de téléphone aléatoire<br/>
* <span style="color: #32977E">=(ALEA.ENTRE.BORNES(1;28)&"/"&ALEA.ENTRE.BORNES(1;12)&"/"&ALEA.ENTRE.BORNES(1970;1999))</span> : date de naissance aléatoire<br/>

Cela nous permet d'étoffer les informations liées aux USERS.

#### --- Mise en place d'une GPO pour autoriser les mdp faibles --- <a name="IIIB4"></a>

- Gestion de stratégie de groupe
- Objet de stratégie de groupe
- Stratégie Default Domain Policy
- Modifier
    -> Paramètre / Config ordi / Stratégies / Paramètres windows / Paramètres de sécurité / Stratégie de compte / stratégie de mdp <br/>
    -> changer les règles de mdp pour que les mdp générés via PIN (1234) soient acceptés

![Accès aux Stratégies de groupes](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/gestion_strat%C3%A9gies_groupes.jpg)

![Baisse du niveau de sécurité des mdp via GPO](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/restrictions_mdp.jpg)

![On force les modifications de la GPO](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/update%20_force.jpg)

#### --- Générer les users créés dans le GLPI via un script shell --- <a name="IIIB5"></a>

Le script devra avoir l'extension .ps1 c'est-à-dire powershell version 1, qui permet la plus grande compatibilité.

* Script PS1 : [Script sur cefim](https://campus.cefim.eu/pluginfile.php/54105/mod_resource/content/1/adimport.ps1)
* Script PS1 simplifié 

```ps1
$users = import-csv -path "C:\Users\TSSR\Desktop\import.csv" -delimiter ";"
foreach($user in $users)
{
    $prenom = $user.prenom
    $nom = $user.nom

    $nomComplet = $prenom + " " +$nom
    $idSAM = $prenom.substring(0,1) + $nom
    $id = $idSAM + "@tssr.lan"
    $email = $idSAM + "@tssr.lan"

    $pass= ConvertTo-SecureString "1234" -AsPlaintext -Force

    New-ADuser -name $idSAM -DisplayName $nomComplet -givenname $prenom -surname $nom -EmailAdress $email -Path "OU=usagers,DC=tssr,DC=lan -UserPrincipalName $id -AccountPassword $pass -Enabled $true
}

```

- Ouverture via NotePad++
- On met le fichier csv (**import.csv**) et le fichier ps1 (**script.ps1**) sur le bureau 
- On lance l'invite de commande PowerShell
> `Set-Location C:\Users\TSSR\Desktop\`<br/>
> `./script.ps1`<br/>

- On vérifie dans l'AD chez les usages : la liste a bien été générée

Pour le mappage des infos csv/ad : [SIte de microsoft qui donne le nom des catégories afin de permettre de rajouter des variables dans le script pour l'import d'infos supplémentaires](https://docs.microsoft.com/fr-fr/system-center/scsm/ad-ds-attribs?view=sc-sm-2019)
