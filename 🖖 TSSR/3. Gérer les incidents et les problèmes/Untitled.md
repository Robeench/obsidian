
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


## V. Configuration et utilisation de GLPI <a name="IV"></a>

Dans le chemin `/windows/system32/drivers/etc/` il y a un fichier *services* où toutes les infos ports sont dedans + fichier *hosts* où il est possible de filtrer le réseau via ip/nomdns (sert de DNS local)

### A) Mise en lien d’Active Directory et de notre GLPI via DNS <a name="IVA"></a>

<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>


- [DNS et Windows Server](https://openclassrooms.com/fr/courses/2356306-prenez-en-main-windows-server/5835581-installez-un-serveur-dns)<br/>
- [DNS dans AD](https://blog.netwrix.fr/2020/07/29/dns-dans-active-directory/)<br/>

</details>

Il s'agire de faire en sorte que les machines puissent avoir accès via une résolution des noms de domaines aux différents server et vice-versa. Ainsi il faudra que nous permettions aux différents services DNS d'être raccord entre les noms de domaines et les IP que nous souhaitons liées.

#### --- Mise sous tutelle du Wserveur via protocole DNS --- <a name="IVA1"></a>

Ajouter un support glpi dans WServer2019 + une redirection DNS car il faut mettre notre WServeur sous tutelle du DNS. POur se faire nous allons ajouter un support glpi dans WServer2019 ainsi qu'une redirection DNS

1. Pannel / DNS / gestion / DC1 / Zone de recherche directe / tssr.lan / Nouvel hôte
-> support_glpi + 192.168.0.32(adresse serveur glpi)<br/>
-> http://support_glpi.tssr.lan (accès au support via une adresse http)<br/>

![Support_glpi](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/support_glpi.png)

Ainsi, nous mettons en lien via notre nom de domaine tssr.lan l'ip de notre server glpi via son adresse IP fixe.

![Support glpi](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ajout_support_dns.jpg)

2. Sur la machine hôte faire pointer le DNS vers l'IP du WServeur (192.168.0.33) pour que ça fonctionne aussi sur la machine hôte

#### --- Modifications du DNS de réponse sur le serveur GLPI via VM Debian --- <a name="IVA2"></a>

1. Modifier le serveur de résolution dns dans le serveur glpi (ici, IP de notre serveur AD)

2. Aller sur la machine GLPI
> `nano /etc/resolv.conf` <br/>
-> serveur dns = ip wserveur = 192.168.0.33

Ainsi, le server GLPI qui est hébergé sur notre VM debian résout sa recherche DNS directement via notre WServer. Nos deux serveurs (GLPI-WServer) sont donc désormais liés dans la résolution DNS de leurs IP.

### B) Import des users via un annuaire LDAP <a name="IVB"></a>

1. Via l'interface GLPI
- Configuration / Authentification / Annuaires LDAP
- Nom : **tssr.lan**
- Serveur : **dc1.tssr.lan**
- OU=usagers,DC=tssr,DC=lan
- administrateur@tssr.lan / mdr=mdp de WServeur2019 (Admin7007)

2. Utilisateurs
- Utilisateurs / Annuaires LDAP / Importer les usagers

![Import des users](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/import_user_glpi.jpg)


### C) Configurer entité(s) et intitulés <a name="IVC"></a>


<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>

* [Configurer les intitulés](https://glpi-project.org/DOC/FR/glpi/config_dropdown.html)<br/>
* [Via le site GLPI](https://glpi-user-documentation.readthedocs.io/fr/latest/modules/configuration/intitules/index.html)<br/>
* [Injection en masse des données dans GLPI](https://neptunet.fr/glpi-data-injection/)<br/>

</details>


1. On commence par changer l'entité 
-> Nom : **bortzmeyer** comme entité racine (ou alors en *enfant*)
-> Infos générales rentrées (Adresse)
-> Règles génériques = tag = n°pour équipements qui représente quelque chose qui pourrait servir pour inventaire

![Info entité](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/entit%C3%A9.jpg)

- Ensuite on passe aux intitulés 
* ([Lien Dell pour aport fabricants et config via it.zero.fr](https://it.izero.fr/glpi-ajout-plugin-imports-fabricants-et-configuration-pour-dell/))
    -> bien lister les ensembles d'infos
    -> ex: OS (Windows, BSD, Linux...), Type d'ordinateur (Laptop, PC...)

![liste d'intitulés](https://github.com/cromm24/Hello_World/blob/GLPI/intitul%C3%A9s.jpg?raw=true)

![Intitulés remplis, exemple](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/intitul%C3%A9s%20replus.png)


#### D) Gestion générale de GLPI : plugins <a name="IVD"></a>


<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>

* [Gestion générale de GLPI](https://neptunet.fr/glpi/)<br/>
* [Cours OpenClassroom sur FusionInventoy](https://openclassrooms.com/fr/courses/1730516-gerez-votre-parc-informatique-avec-glpi/5994176-installez-le-plugin-et-l-agent-fusioninventory)<br/>
* [Liste des PLugins dispo](https://plugins.glpi-project.org/#/)<br/>
* [Tuto online via Neptunet](https://neptunet.fr/glpi-ad/)<br/>

</details>


Pour installer un plugin dans GLPI, il suffit de télécharger son archive puis de l'extraire dans le dossier .../glpi/plugins, et de les installer via l'interface de GLPI. Ensuite, dans l'interface GLPI, aller sous Configuration > Plugins cliquez sur Installer puis Activer. À noter qu'un plugin peut disposer de plusieurs versions, chaque version est la plupart du temps spécifique à une version précise de GLPI


1. [DataInjection](https://neptunet.fr/glpi-data-injection/)

```

cd /tmp
wget https://github.com/pluginsGLPI/datainjection/releases/download/2.9.0/glpi-datainjection-2.9.0.tar.bz2
tar -xvjf glpi-datainjection-2.9.0.tar.bz2
cp -r datainjection/ /var/www/html/plugins/
chown -R www-data /var/www/html/plugins

```

2. Dashboard

```

cd /tmp
wget https://forge.glpi-project.org/attachments/download/2323/glpi-dashboard-1.0.2.zip
unzip glpi-dashboard-1.0.2.zip
cp -r glpi-dashboard-1.0.2/ /var/www/html/plugins/

cd /var/www/html/plugins/
mv glpi-dashboard-1.0.2 dashboard

chown -R www-data /var/www/html/plugins

```

3. Fusion inventory plugin pour déployer agents

```

cd /tmp
wget https://github.com/fusioninventory/fusioninventory-for-glpi/archive/refs/tags/glpi9.5+3.0.tar.gz
tar -xvjf fusioninventory-9.5+3.0.tar.bz2
cp -r fusioninventory/ /var/www/html/plugins/
chown -R www-data /var/www/html/plugins

```

![FusionInventory](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/plugins.jpg)  

4. Crontab (suite à l'installation de Fusion Iventory)

**Crontab** sous Linux est la table qui gère les actions automatiques. Pour que GLPI puisse fonctionner “automatiquement” malgré son aspect de site en PHP (qui ne réagit donc que quand il y a une requête), on intègre un fichier cron.php qui va envoyer automatiquement une requête toutes les minutes sur le serveur, pour simuler la présence de quelqu’un sur la page.

> `cd /root`
> `# crontab -u www-data -e` <br/>
-> Choix n°1 pour use nano

On ajoute à la fin la ligne

```
*/1 * * * * /usr/bin/php7.3 /var/www/html/front/cron.php &>/dev/null

```

Ensuite
> `# /etc/init.d/cron restart`


#### E) Gestion générale de GLPI : mise en pratique via FusionIventory <a name="IVE"></a>

* Téléchargement de FusionInventory Agent via [GitHub](https://github.com/fusioninventory/fusioninventory-agent/releases/download/2.6/fusioninventory-agent_windows-x64_2.6.exe)  
* On l'installe sur notre client
    - Choisir les composants : **complète**
    - Choisir la destination (serveur GLPI) : http://192.168.0.32/plugins/fusioninventory/  et cochez installation rapide   

* On va sur http://localhost:62354 
* On force une remontée : **Force an inventory**

* Ensuite on va sur le GLPI de son hôte et dans Ordinateur on peut voir la remontée (ici, **DC1** puisqu'à partir de notre WServeur dont le nom est DC1)

![Voici ce que cela donne via l'interface GLPI](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/Capture%20d%E2%80%99%C3%A9cran%202021-06-23%20155415.jpg)

Et on répète l'action sur des VM agents sous W10 créées pour l'occasion (192.168.0.41 et 192.162.0.42, avec en passerelle/dns notre WServer 192.168.0.33). 

![Agent DC2](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/agentsw10.jpg)

On utilise le partage de dossier VMware pour lancer FIAgent et on pousse des remontées.
Idem avec le smartphone et l'application GLPI Agent.

![Import via FusionInventory](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/import%203%20agents.png)

On peut ensuite faire un état des lieux de l'ensemble du parc (le gsm est reconnu comme ordinateur)

![Tableau de bord du GLPI local avec les imports](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tableau%20de%20bord%20glpi.png)


#### F) Gestion générale de GLPI : tickets et création d'un Helpdesk <a name="IVF"></a>


<details>
<summary markdown="span">Ressources web, cliquez ici pour y accéder</summary>

* [OpenClassroom](https://openclassrooms.com/fr/courses/1730486-gerez-vos-incidents-avec-le-referentiel-itil-sur-glpi/6544671-traitez-et-suivez-votre-ticket-dans-glpi)<br/>
* [GLPI-Project](https://glpi-project.org/DOC/FR/glpi/helpdesk_openticket.html)<br/>
* [HelpDesk ticket](https://glpi-project.org/DOC/FR/glpi/helpdesk_ticket.html)<br/>
* [Cours AFPA sur gestion de tickets](https://github.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/blob/pdf/Gestion-des-tickets-dans-GLPI(1).pdf)

</details>


Le module d'assistance de GLPI est conforme au guide de bonnes pratiques ITIL pour la partie Gestion des incidents et gestion des demandes de services : il intègre donc des notions comme l'impact, l'urgence d'un ticket, la matrice de calcul des priorités associées et une normalisation des statuts. Bien que l'outil soit conforme ITIL, il n'y aucune obligation pour suivre ces bonnes pratiques : chacun est libre d'implémenter la gestion des incidents qui correspond le mieux à ses besoins.


1. Création d'un ticket :  

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/creation_ticket.jpg)

2. Deux exemples de résolutions de tickets :  

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/r%C3%A9solution%20ticket.png)  

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket_r%C3%A9solu.jpg)  

Il est possible de voir l'ensemble des tickets dans l'interface GLPI.

![Récapitulatif des tickets](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tockets.png)

3. Exemples de résolutions de tickets dans un contexte d'entreprise et avec une réelle perspective de résolution informatique

![Accès au ticket](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/creer%20un%20tiket.jpg)

![Demande en cours](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/r%C3%A9solution%20ticket%202.png.jpg)

![Réponses aux question](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/ticketre%C3%A7u2.jpg)

* Ticket Michie

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket1michie.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket2michie.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket3michie.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket4michie.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket5michie.jpg)

* Ticket Michu

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket2michu.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/ticket3michu.jpg)

![*](https://raw.githubusercontent.com/cromm24/Hello_World/GLPI/tticket4michu.jpg)


#### G) Gestion générale de GLPI : tickets et création d'un Helpdesk dans le cloud <a name="IVG"></a>


* Remplissage ddu GLPI commun (https://support.cefim.ninja)
    -> rdelmas (admin)
    -> glagaffe (noobuser)

![Tableau récapitulatif](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tableau_sujets_glpi.png)

- On créé les tickets en fonction des problèmes rencontrés
- On attribue ensuite les tickets aux personnes dédiées

![Mise à disposition des tickets](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/creation%20de%20deux%20tickets%20et%20attribuation%20%C3%A0%20charles.jpg)

Ensuite on organise l'assistance à distance.

1. **Ticket 1**

![Echanges entre technicien et usager](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/ticket%20r%C3%A9solu.png)

![L'usager confrme la réparation](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/ticket%20resolu.png)


1. **Ticket 2**

![Echanges entre technicien et usager](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tik2.png)

![L'usager confrme la réparation](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tik2b.png)


#### H) Création d'une FAQ <a name="IVH"></a>


<details>
<summary markdown="span">Ressources web et AFPA, cliquez ici pour y accéder</summary>

- [Base de connaissance et FAQ](https://glpi-project.org/fr/base-de-connaissances-et-foire-aux-questions-faq/)<br/>
- [Tools Knowbase via glpi-project](https://glpi-project.org/DOC/FR/glpi/tool_knowbase.html)<br/>
- [Cours AFPA sur la FAQ](https://github.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/blob/pdf/base-de-connaissance-GLPI(1).pdf)(br/>)

</details>


La base de connaissances répond à deux objectifs principaux : Le premier est de centraliser des connaissances internes aux différents techniciens. Le second est de mettre à disposition des utilisateurs des informations (FAQ publique) leur permettant de résoudre seuls des problèmes simples.

Seuls les éléments de la FAQ publique sont visibles par les utilisateurs de l'interface simplifiée. Les éléments qui ne sont pas définis comme faisant partie de la FAQ publique sont visibles uniquement au sein de la console centrale par des techniciens par exemple. 

* GLPI / Outils / Base de connaissance
    -> possible de parcourir les différents articles via *Parcourir*
    -> pour ajouter appuyer sur "+"

![Ajout topic FAQ](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/Ajout%20faq.png)

* On vérifie ensuite dans l'accès utilisateur

![FAQ 1](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/faq1.png)

![FAQ 2](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/faq2.png)


## VI. Solution ITIL (Axelos) <a name="VI"></a>

ITIL pour Information Technology Infrastructure Library, qui peut se traduire par Bibliothèque de l’Infrastructure des Technologies de l’Information, a été à l’initiative de l’organisation du commerce britannique (OGC) dans les années 80. Actuellement, ce standard est répandu et utilisé dans les plus grandes entreprises et organisations publics à travers le monde.
Un ensemble de bonnes pratiques

ITIL est un ensemble de livres qui regroupe les bonnes pratiques de management d’un service informatique dans le but d’optimiser l’utilisation des ressources informatiques. Ces guides sont une source d’informations permettant d’adapter l’organisation de son service IT à son business. En effet, suivre ce modèle permet de partager un même vocabulaire, d’identifier le rôle de chacun et de professionnaliser l’organisation. La démarche ITIL comprend, dans sa version 3 (ITIL V3), 24 processus traitant de : gestion des problèmes, perspective business/métier, planification de l'implémentation de la gestion de services… pour 4 fonctions :

* Centre de service
* Gestion de technique
* Gestions des opérations
* Gestion des applications

Datant de juin 2007, ITIL V3 est caractérisé par la prise en compte de la virtualisation, l’externalisation ou encore des nouvelles architectures technologiques.
Quels sont les bénéfices pour l'entreprise ?

Le principal objectif de l’ITIL est d’améliorer de manière significative le service au client, c’est pourquoi nous le retrouvons au cœur du modèle, en favorisant l’efficacité des fonctions informatiques. L’adoption du modèle apporte de nombreux avantages à l’entreprise utilisatrice :

* Gain de temps
* Réduction des coûts
* Définition des rôles et responsabilités plus précises
* Meilleure satisfaction des utilisateurs
* Meilleure productivité/efficacité
* Services IT de meilleures qualités
* Adaptation aux besoins des clients facilitée

Aujourd’hui, plus d’un million de professionnels sont formés et certifiés ITIL. Bien qu’il existe des alternatives comme COBIT, l’ITIL est reconnu comme la méthode la plus performante en termes de gestion des services dans le monde.

<details>
<summary markdown="span">Ressources AFPA, cliquez ici pour y accéder</summary>

* [ITIL-GestionIncidents](https://github.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/blob/pdf/ITIL-GestionIncidents.pdf) <br/>
* [Sensibilisation à ITIL](https://github.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/blob/pdf/Sensibilisation-a-ITIL.pdf) <br/>

</details>


### A) Première approche <a name="VIA"></a>


* Définition

[![ITIL®: qu'est-ce que c'est? 5 minutes pour comprendre](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/video1.png)](https://www.youtube.com/watch?v=gpfgJW8fr7g)


* Introduction

[![Introduction à ITIL® et aux meilleures pratiques informatiques](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/video2.png)](https://www.youtube.com/watch?v=hbascBS1esU)

<br/>

1. Définition ITIL : 9'30 - 18'35 <br/>
2. Processus incident : 20'07 - 22'35 <br/>

N'a pas pour objectif de comprendre pourquoi mais d'assurer la continuité de service. l'incident doit géner le moins possible le client. (ne pas s'accès sur la technique). L'ordre de répartation se fait en fonction de la necessité et non du cout.  

3. Processus Gestion de service/SLA/OLA (alignement sur les priorités du métier) : 23'07 - 27'22 <br>

Un SLA : c'est un contrat Service Level Agrement : codifie la relation entre le fournisseurr de service et le client. Definisse les obligations de l'un et de l'autre. Help desk = Accord sur les niveaux opérationnels (OLA Opérationnal Level Service ). Grace à ces SLA je vais pouvoir definir uun priorité d'urgence.

4. Processus Gestion de catalogue de services : 27'30 - 32'46 <br/>

Gestion de catalogue de processus: délimité le rôle et les services délivrés par l'IT. Ce processus est Divisé en deux parties : 
- la partie business, obtenir une imprimante, un renouvellement de PC,etc ...
- La partie technique: services utilisés en interne par l'IT pour forrnir le services business.  (masterisation d'un PC, Livraison du PC etc ...)
    -> service de base qui fournit les résutlat essentiels  
    -> service de soutien : service qui fournis le service de base
    -> service réhaussé : service qui ajouté au service de base apporte une valeur ajouté.  

5. Processus Gestion des changements : 33'00 - 35'35 <br/>

Gestion des changement : tech et organisationnel.  
- Changement standard : changer les choses qui n'ont pas d'impact  
- Changement urgent :  ex mise en production et il y a un probleme qui vas crée un grave disfonctionnement ou une perte de donnée.  
- Changement normal : pour tout le reste  

6. Processus Gestion des configurations (SACM) : 35'35 - 40'07 <br/>

<br/>

ITIL est la meilleure pratique la plus aboutie pour gérer les processus informatiques d'une entreprise  

- Information Technologie Infrastructure Library
- Stratégie
- Conception
- Transition
- Exploitation
- Amélioration Continue

C'est devenu un prérequis dans les ESN : le niveau fondation 2/3j : base d'ITIL.

- Niveau intermediaire lifecycle : w sur les différents détails du processus
- SS: service Stratégie
- Service Design
- Service Transition
- Service Opération
- CSI Continu Service Improvement 
- 3j par crusus avec examen

ITIL est le moyen de nous structuerer de maniere à fournir des services
de passer à l'inforrmatique fournissant de  la technologie à l'informatique de service artisanal vers l'insdustriel.



### B) Appliquer les bonnes pratiques en centre de services (ITIL) <a name="VIB"></a>

#### --- Objectifs --- <a name="VIB1"></a>

ITIL (Information Technology Infrastructure Library) est un ensemble de bonnes pratiques pour améliorer la production informatique au service des objectifs métiers de l'entreprise.

A l'issue de cette séance, le stagiaire sera capable , dans le cadre d'un centre de services (Hotline ou HelpDesk), de mettre en œuvre les processus de gestion d'incidents et de problèmes et communiquer avec l'équipe en charge du support aux utilisateurs dans un langage commun ITIL.

Lors de la résolution d'incidents ou problèmes avec un logiciel de gestion d'incidents (comme GLPI), le stagiaire sera capable de documenter correctement les incidents en se référant à ce vocabulaire ITIL .

Les processus ITIL visés dans cette séance sont ceux de la phase Exploitation de Services (Gestion des incidents, Gestion des problèmes, Gestion des événements, ...) et de la phase Transition de Services (Gestion des configuration, gestion des connaissances,...).

#### --- Consignes --- <a name="VIB2"></a>

Assurez-vous que vous avez déjà saisi un ticket incident précédemment lors de la séance "Utiliser le logiciel de gestion d'incidents (GLPI)" et que la base de problèmes et de connaissances est déjà alimentée. Si ce n'est pas le cas alimentez la base par des exemples types.

Le stagiaire après lecture des documents "Sensibilisation à ITIL" et "ITIL-GestionIncidents" (voir ci-dessous) est amené à identifier le vocabulaire concrètement en analysant un ticket, un problème et un élément de la base de connaissances.

 
#### --- Vocabulaire --- <a name="VIB3"></a>

La prise en charge professionnelle du support aux utilisateurs, exige des bonnes pratiques et l'adoption d'un vocabulaire commun à une équipe de Hotline ou Help Desk décrit dans le référentiel ITIL. En étudiant les documents "Sensibilisation à ITIL" et "ITIL-GestionIncidents" vous découvrirez ce référentiel et les termes couramment utilisés dans un service d'assistance.

Vous pouvez approfondir ce sujet en consultant le site Itil France : http://www.itilfrance.com/ et vos propres recherches sur Internet.

Créez votre propre lexique des termes ITIL les plus importants dans le contexte du métier de l'assistance aux utilisateurs à retenir, à titre d'exemple :


<details>
<summary markdown="span">Glossaires ITIL, cliquez ici pour y accéder</summary>

* [Glossaire ITIL](https://wiki.octopus-itsm.com/fr/articles/Glossary)
* [Glossaire ITIL 2](https://www.itpms.fr/wp-content/uploads/2018/03/ITIL_2011_Glossary_FR-v1-1.pdf)

</details>


1. Définitions officielles

* **Centre de services** : Le centre de services (CDS) est une fonction (au sens « département de l’entreprise ») de service d'assistance informatique de la partie « Soutien des Services » des bonnes pratiques ITIL. Son objectif est de servir de guichet unique aux utilisateurs pour leurs besoins de services informatiques. 
La pratique Centre de services, en anglais service desk, est le point de contact unique entre les utilisateurs et le département informatique. Il est porteur de toute la relation avec les utilisateurs. Cette relation est bidirectionnelle : les utilisateurs appellent le centre de services pour communiquer avec le département informatique et lorsque celui-ci veut envoyer des messages d’information aux utilisateurs, il fait appel au centre de services. Le centre de services est responsable de l’information des utilisateurs au quotidien

* **Fonction** : Une fonction est une unité organisationnelle avec ses ressources et ses moyens propres. C’est une équipe ou un ensemble d’équipes, avec un responsable qui les dirige. Une fonction est spécialisée dans la réalisation de certains types de travaux et garantit les résultats obtenus. Une fonction va prendre en charge une ou plusieurs activités d’un ou plusieurs processus. Une fonction est responsable des outils qu’elle utilise tant pour leur définition, leur choix et leur mise en œuvre. Une fonction sert à stabiliser les organisations.

* **Processus** : Les processus ITIL (Information Technology Infrastructure Library, ou Bibliothèque pour l’infrastructure des technologies de l’information en français) est un recueil de bonnes pratiques visant à améliorer le management des services informatiques (ITSM).

* **Rôle** : Un rôle est un ensemble de responsabilités et de domaines d’autorité attribués à un poste. Un rôle est un comportement face à une activité. Ce rôle va être ensuite affecté à une personne physique ou à une équipe de personnes. En règle générale, un rôle est défini dans un processus ou une fonction. Certains rôles sont liés aussi aux services. On va donc identifier des rôles qui sont détenus par les clients ou par les utilisateurs. Une personne physique ou une équipe de personnes peut endosser plusieurs rôles. Par contre les bonnes pratiques précisent que certains rôles sont incompatibles entre eux. On verra des exemples dans les chapitres suivants. On peut d’ores et déjà citer le rôle du gestionnaire des incidents qui ne doit en aucun cas être porté par la même personne que le rôle du gestionnaire des problèmes.

* **SLA** : La gestion des niveaux de service (en anglais SLM, Service Level Management) a pour but de maintenir et améliorer progressivement la qualité des services informatiques indispensables aux activités de l’entreprise. Le tout en s’assurant que les réalisations sur le plan des services soient soumises à un cycle d’approbation, de contrôle, de rapports et de révisions, et que les mesures nécessaires soient prises pour éliminer les niveaux inacceptables de service. Accords sur les niveaux de service (service level agreement ou SLA): ce sont les accords définis entre l’informatique (fournisseur) et le business (clients) pour déterminer les niveaux de prestation d’un service.

* **KPI** : En anglais, un KPI est un Key Performance Indicator. En français, c'est un indicateur clé de performance (ICP). Le KPI est là pour mesurer au fil du temps, afin de pouvoir se comparer à des entreprises similaires et de déterminer si l'on progresse ou si l'on régresse. L'objectif étant bien sûr de progresser et de ne pas être "à la traîne" par rapport à ses concurrents.

* **Gestion des Incidents** : La gestion des incidents a pour but de rétablir la communication entre les utilisateurs finaux et les agents informatiques au sein d'un service desk informatique, et de garantir la fluidité des opérations. L'entreprise suit un ensemble de bonnes pratiques pour gérer et résoudre les incidents de manière efficace. Celles-ci font partie du référentiel ITIL, qui vise à améliorer l'efficacité des services et la productivité. 


* **Gestion des Problèmes** : « La gestion des problèmes vise à réduire le taux de probabilité et l’impact des incidents grâce à l’identification de leurs causes plausibles et effectives ainsi qu’à la gestion des contournements et des erreurs connues. ». La gestion des problèmes vous pousse à aller plus loin que la simple résolution d’incidents en exigeant d’identifier le problème à l’origine de cet incident. En conclusion, investir du temps et de l’argent dans la gestion des problèmes maintenant, c’est gagner du temps et de l’argent à terme. CQFD.

* **Gestion des Configurations** : Selon ITIL, le but de la Gestion des Configurations est de fournir un modèle logique de l’infrastructure IT en identifiant, contrôlant, maintenant à jour et vérifiant les versions de tous les Eléments de Configuration (CI) existants. La Gestion des Configurations se positionne au coeur d’une gestion efficace des services informatiques. Plus qu’un simple registre des biens informatiques, elle inclut la documentation, les accords de niveaux de service, les catalogues de service, les garanties et les articles de la Base de connaissances. Ainsi, la Gestion des Configurations fournit un service d’information facilitant la planification, la Mise en Production et la mise en oeuvre efficace et efficiente des Changements de service en informatique.

* **Erreur connue** : Une erreur connue décrit la solution de contournement permettant de résoudre (de façon temporaire ou permanente) des dysfonctionnements. Généralement, elle est mise en place suite à l'apparition d'un problème à l'origine d'incidents, mais elle peut également être créée en amont. Ainsi, via ITIL Enregistrement d'une erreur connue : une fois le diagnostic complété et une solution temporaire ou permanente identifiée, le problème devient une erreur connue. Ainsi, si d'autres incidents ou problèmes surviennent, ils peuvent être identifiés et le service restauré plus rapidement.

* **Escalade** : L’équipe de support doit-elle obtenir de l’aide de la part d’un autre service ? Si oui, on engage une procédure de demande de service sinon, la résolution de l'incident s’effectue au niveau du support initial.

* **Base de connaissances** : La mission du processus de la gestion de la connaissance est de fournir une information compréhensible et fiable pour permettre la prise de décisions à tous les instants du cycle de vie. Ce processus a un vrai objectif d’améliorer l’efficience dans toute la démarche ITIL, en mettant à disposition des autres processus un système de gestion de la connaissance (SKMS, Service Knowledge Management System).

* **CMDB** : Une base de données de gestion de configuration (Configuration Management Data Base) est un référentiel qui sert d'entrepôt de données pour les installations IT. Il contient des données relatives à un ensemble des actifs IT (communément appelés éléments de configuration ou configuration items (CI)), ainsi que des relations descriptives entre ces actifs. Une CMDB fournit une vue organisée des données de configuration et un moyen d'examiner ces données à partir de n'importe quel point de vue. Le dépôt fournit un moyen de compréhension : la composition des actifs critiques tels que les SI (systèmes d’information), les sources en amont ou les dépendances des actifs, les cibles en aval des actifs

* **ITSM** : La gestion des services IT (ITSM) est une approche stratégique permettant de concevoir, de distribuer, de gérer et d'améliorer la manière dont la technologie de l'information (IT) est utilisée au sein d'une entreprise. L'objectif de la gestion des services IT est de garantir la mise en place des personnes, technologies et processus appropriés pour permettre à l'entreprise d'atteindre ses objectifs commerciaux.

* **RFC** : La demande de changement est le point d’entrée du processus de gestion des changements et globalement le point d’entrée de la phase de transition des services. Une demande de changement est un formulaire que le demandeur du changement doit remplir initialement, mais c’est aussi la fiche qui va suivre le changement jusqu’à sa clôture. De ce fait ce formulaire sera complété par le gestionnaire des changements pendant toute la vie du changement. Il faut définir des formulaires...


2. Définitions rédigées par *JB, Bruno, Richard et Romain*


* **Centre de services:** C'est un département de l'IT d'une entreprise qui est dédié au support des utilisateurs.  

* **Fonction:** Une unité organisationnelle avec ses ressources et ses moyens propres. C'est une équipe ou un ensemble d'équipe avec un responsable qui les dirige.  

* **Processus:** Ensemble d'activités structurées conçues pour atteindre un objectif spécifique.  

* **Rôle:** Ensemble de responsabilités, d'activités et d'autorités attribuées à une personne ou à une équipe. Le rôle est défini dans un processus qui lui-même est defini dans une fonction.    

* **SLA:** _Service Level Agrement_: Accord entre un fournisseur de service informatique et un client.  

* **KPI:** _Key Indicator of Perfomance_: Il permet de se comparer à des ESN similaires afin de mesure sa progression ou regression.  

* **Gestion des Incidents:**  Processus qui assure la continuité des servicces. L'objectif est de maintenir l'activité avant de corriger le problème.  

* **Gestion des Problèmes:** C'est l'anticipation des futurs problèmes et de determiner les problèmes récurrents afin de minimiser les impacts.  

* **Gestion des Configurations:** C'est de maintenir à jour tout les éléments composant l'infrastructure IT tels que les MAJ logiciels, la documentation, les contrats, etc...  

* **Erreur connue:** problème pour lequel il existe une documentation sur la ou les causes et ses solutions.  

* **Escalade:** C'est le fait de redirigé un incident que l'on peut résoudre vers le niveau supérieur.  

* **Base de connaissances:** C'est l'ensemble des connaissances des techniciens, de la documentation et des informations détenu par l'entreprise.

* **CMDB:** _Configuration Management DataBase_: Donnée relative à un ensemble des actifs, fournis une vue globale aux données de configuration et de les stockés.

* **ITSM:** _Information Technologie Services Management_: C'est la gestion des services informatiques, qui sont assurés par le centre de services. C'est le services de liaison.  

* **RFC** _Request For Change_: Point d'entrée du processus des changements. C'est le document initial qui régis et lance la demande dans une infrastructure.  


3. Définitions rédigées (*Réalisé par Julie, Nicolas, Hamza et Rémi*)


* **Centre de services**: Le service desk, ou centre de service IT, est conçu pour faire la liaison entre les utilisateurs au quotidien. Tout passe par le centre de service, pas de passe droit ou priorité car je connais.exemple utilisation de GLPI.

* **Fonction** : Une fonction est une unité organisationnelle avec ses ressources et ses moyens propres. C’est une équipe ou un ensemble d’équipes, avec un responsable qui
les dirige. Une fonction est spécialisée dans la réalisation de certains types de travaux et garantit les résultats obtenus. Une fonction va prendre en charge une ou plusieurs activités d’un ou plusieurs processus. Une fonction est responsable des outils qu’elle utilise tant pour leur définition, leur choix et leur mise en oeuvre. Une fonction sert à stabiliser les organisations.

![Fonction](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/Schema_fonction_processus.png)

* **Processus** : C’est la démarche effectuée entre l'élément d'entrée et de sortie qui est documenté et suivi pour la traçabilité de l’entreprise. Ce qui permet pour une même demande avec la même entré de réutiliser ce processus

![Processus](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tactique%20et%20processu.png)

* **Rôle** : Un ensemble de responsabilités, activités et prérogatives déléguées à une
personne ou une équipe. Un rôle est défini pour un processus

* **SLA** ou « entente de niveau de service » est un document qui définit la qualité de service, prestation prescrite entre un fournisseur de service et un client.

* **KPI ou “Key performance indicator”** sont utilisés pour déterminer les facteurs pris en compte pour mesurer l'efficacité globale d'un dispositif commercial ou marketing ou celle d'une campagne ou action particulière.

* **Gestion des Incidents** : l'objectif de la Gestion des Incidents est la suivante : « Restaurer aussi vite que possible le fonctionnement normal des services et minimiser l'impact négatif sur les activités métiers et s'assurer ainsi que les meilleurs niveaux de qualité de service et de disponibilité sont maintenus. »

![Gestion des incidents](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/gestion%20des%20incidents.png)

* **Gestion des Problèmes** : Gestion des problèmes est le processus responsable de la
gestion du cycle de vie de tous les problèmes. Les objectifs principaux sont de prévenir proactivement que des incidents ne surviennent et minimiser l'impact de ceux qui ne peuvent être évités.

![Gestion des problèmes](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/gestion%20des%20probl%C3%A8mes.png)

* **La gestion des configurations** : c’est un processus destiné à maintenir les systèmes informatiques, les serveurs et les logiciels dans l'état souhaité et à préserver la cohérence de cet état. C'est une façon de s'assurer qu'un système fonctionne comme prévu au fil des changements effectués

* **Erreur connue** : Une erreur connue décrit la solution de contournement permettant de résoudre (de façon temporaire ou permanente) des dysfonctionnements. Généralement, elle est mise en place suite à l'apparition d'un problème à l'origine d'incidents, mais elle peut également être créée en amont.

* **Escalade** : Action de transférer un incident, un problème ou un changement à une équipe technique possédant un plus haut degré d’expertise afin d’aider le processus d’escalade. L’escalade peut être nécessaire au sein de tout processus de gestion des services informatiques, mais est le plus souvent associée à la Gestion des Incidents, à la Gestion des Problèmes et à la gestion des plaintes des clients. Il y a deux types d’escalades : escalade fonctionnelle et escalade hiérarchique.

* **Base de connaissances**: Une base de connaissance sert à regrouper des connaissances spécifiques de manière centralisée accessible sur un ordinateur.

* **CMDB** : Change Management Database ou Configuration Management Database en
français est une base de données unifiant les composants d’un système informatique qui
permet également d’en comprendre l’organisation et d’en modifier la configuration. Elle contient des informations sur les principaux composants du système d’information.

* **ITSM** : IT Service Management ou La gestion des services informatiques décrit une
approche stratégique de la conception, la livraison, la gestion et l’amélioration de la façon d’utiliser les technologies de l’information dans l’entreprise. Le but de toute structure de gestion des SI est de s’assurer que les processus, les personnes et la technologie adéquats soient présents afin que l’entreprise puisse atteindre ses objectifs métier.

* **RFC** : Requests for Comments ou Demande de Commentaires, sont une série
numérotée de documents décrivant les aspects et spécifications techniques d’internet ou de différents matériels informatiques comme un routeur ou un serveur DHCP. Les RFC sont classées selon cinq classifications qui sont :
    -> Obligatoire
    -> Recommandée
    -> Facultative
    -> Limitée
    -> Non recommandé
Il y a également trois niveaux de maturité :
    -> Standard proposé
    -> Standard brouillon
    -> Standard internet
Lorsqu’un document est publié, un numéro de RFC lui est attribué et en cas d’évolution un nouveau document sera publié sous une autre référence.


### --- Création d'un questionnaire --- <a name="VIB4"></a>


- [Lien vers les réponses au formulaire](https://forms.gle/azqCk9RnQavB8FiG9)
- [Lien vers un autre formulaire](https://docs.google.com/forms/d/e/1FAIpQLSdeIMhN3JlwuzXQW9CgAbJreGVN3uV2xpx_SHYEjemupWY4XA/viewform)

![Réponses au questionnaire](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/questionnaire.png)


- **Corrigé** :


| questions | réponses | corrigé | 
|------------:|-------------:|-------------:|
| 1 | 1, 3, 4 | 1, 3, 4 | 
| 2 | 4 | 3 | 
| 3 | 2 | 2 | 
| 4 | 2 | 2 | 
| 5 | 1 | 1 | 
| 6 | 1 | 4 | 
| 7 | 1, 3 | 1, 3 | 
| 8 | 1 | 2 | 
| 9 | 2, 3, 5 | 2, 4, 5 | 
| 10 | 2, 3 | 2, 3 | 




---

<a name="VII. Lexique"></a>

## Petit récapitulatif des commandes importantes sur Linux

1. [Index en ligne des lignes de commandes Linux](https://opensharing.fr/index-des-commandes-linux)
2. [Commandes USERs](https://doc.ubuntu-fr.org/commande_shell)
3. [Commandes utilisateurs](http://www2.ift.ulaval.ca/~beaulieu/linux/fr/man1/_index.html)
4. [Les commandes fondamentales de Linux](http://wiki.linux-france.org/wiki/Les_commandes_fondamentales_de_Linux)


<br/>

![Lexique Linux](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/TD6_fwunixrefshot.png)

<br/>

___LEXIQUE___
| commande | explications |
|------------:|-------------:|
| `nmap` | permet de vérifier si les services et port sont ouverts. |
| `zip` | les formats les plus populaires sur linux sont bz bz2 et gz. | 
| `lynx` | permet d'avoir un navigateur en html interprété standard. | 
| `curl` | c'est le programme préféré de l'idôle de Thomas (fallait suivre) permet de tester des url. | 
| `net-tools` | des outils réseaux. |
| `dnsutils` | pour les dns quoi. |
| `bsdgames` | une suite de jeux en ligne de commande. |  
| `samba` | permets de faire du partage à la windows |
| `winbid` | liaison à la windows, notre serveur pourra partager des paquets à la windows |  
| `nsswitch` | name service au sens global de résolution de nom; sert à être vu dans le partage windows et avoir accès au nom netbios |  
| `webmin` | permet d'administrer un serveur linux par un navigateur web (pour les débutants) |  
| `bash` | bourne again shell |  
| `nano` | not another notpad |  
| `wget` | windows obtenir : vas chercher sur le net pour le télécharger |  
| `su -` | permet de passer en super utilisateur mais permets de modifier les variables du path |  
| `dpkg` | debian package |  
| `wbmin` | web administration |  
| `~` | dit qu'on est dans le répertoire maison |  
| `#` | indique qu'on est en power user |