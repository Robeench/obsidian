
# Linux
## Configuration Linux
Changer le nom de la machine :
[Changer le nom (hostname) d'une machine Ubuntu, Debian ou d'un système basé sur eux](https://geekonweb.fr/changer-le-nom-hostname-dune-machine-ubuntu-debian-ou-dun-systeme-base-sur-eux.html)
Changer le workgroup et installer SAMBA :
[How to Change a Workgroup in Linux](https://www.brighthub.com/computing/linux/articles/77964/)

Comment changer [[IP]], gateway, [[DNS]] :
[How to configure Static IP on Debian](https://www.snel.com/support/how-to-configure-static-ip-on-debian-10/)

Bureau à distance :
[How To Install XRDP (Remote Desktop) on Debian 10](https://tecadmin.net/how-to-install-xrdp-on-debian-10/)

Se connecter en [[SSH]] à un serveur distant depuis [[Windows]] :
[Se connecter en SSH en serveur distant](https://www.malekal.com/comment-se-connecter-en-ssh-a-un-serveur-distant-windows/)

Partage de fichiers Linux :
[Comment partager des fichiers entre [[Windows]] et Linux - phhsnews.com](https://www.phhsnews.com/how-to-share-files-between-windows-and-linux4290)

[[Protocole]] [[SMB]]
[Le protocole SMB pour les débutants | IT-Connect](https://www.it-connect.fr/le-protocole-smb-pour-les-debutants/)
[Consultation de fichiers sur un serveur ou un réseau partagé](https://help.gnome.org/users/gnome-help/stable/nautilus-connect.html.fr#urls)

Installation de webmin :
[Install Webmin on Debian 11 - kifarunix.com](https://kifarunix.com/install-webmin-on-debian-11/)

Utilisation de webmin :
[webmin Wiki ubuntu-fr](https://doc.ubuntu-fr.org/webmin)

# Découvrir les terminaux Linux
Les serveurs Linux que l’on administre sont majoritairement dépourvus d’interface graphique, car ce n’est pas nécessaire pour les exploiter les services hébergés sur ces machines.

Pour interagir avec le système et le matériel, l’administrateur utilise un **terminal**.

Autrefois c’était des terminaux physiques, désormais ce sont des terminaux virtuels ou des émulateurs de terminaux.

## [[Virtualisation]] du terminal de commande
Le logiciel simule l'équipement terminal physique et toutes ses fonctionnalités. Il est donc possible de lancer plusieurs terminaux en même temps.

Le protocole VNC ([Virtual Network Computing](https://openclassrooms.com/fr/courses/1733046-prenez-le-controle-a-distance-dun-poste-linux-windows-avec-vnc)) permet notamment de prendre la main à distance sur un ordinateur. C’est un [[Protocole]] de terminal virtuel graphique.

Le [[Protocole]] RDP ([Remote Desktop Protocol](https://fr.wikipedia.org/wiki/Remote_Desktop_Protocol)) qui permet de se connecter sur des serveurs [[Windows]] Terminal Serveur en est un également.

L’écran noir après le démarrage du système est aussi un terminal. On l’a nommé historiquement une **console**. La console de Linux propose 7 terminaux en mode texte, appelés aussi les terminaux physiques. Ils sont directement sur le clavier branché à l'ordinateur et disponibles à partir des combinaisons de touches : `CTRL+ALT+F1` ; `CTRL+ALT+F2` ; … jusqu’à `CTRL+ALT+F7`. Chacune de ces combinaisons de touches propose l'émulation d'un terminal (en mode console) différent sur lequel il est possible de se connecter de manière indépendante avec un compte utilisateur différent.

## Les principaux émulateurs de terminal
Un émulateur de terminal permet de se connecter avec un protocole réseau sur le serveur distant autant de fois que souhaité, y compris sur le même serveur avec des utilisateurs différents.

### [[Windows]]
[[Windows]]
-   **PuTTY** est à la fois un émulateur de terminal et un client pour différents protocoles réseau tels que telnet, SFTP, [[SSH]], rlogin, et TCP.
-   **[[Windows]] Terminal**

### MacOS
[[MacOS]]
-   **MacOS** étant un dérivé de la branche historique BSD (Berkeley Software Distribution) des Unix communautaires universitaires, l'émulateur de terminal est dans un milieu natif : l'application est livrée par défaut avec le système.

### Linux
[[Linux]]
-   **xterm**, c'est un peu le papy de la famille. Ce programme émule les terminaux VT102/VT220 de [DEC (Digital Equipment Corporation)](https://fr.wikipedia.org/wiki/Digital_Equipment_Corporation), les successeurs du terminal VT100 illustré un peu plus haut. Beaucoup d'émulateurs présentés dans cette section sont des variantes de xterm.
-   GNOME propose **[GNOME Terminal](https://help.gnome.org/users/gnome-terminal/stable/)**. C’est un grand classique également qui, outre les fonctionnalités de son grand-père, est livré avec la gestion des onglets, la transparence et les fonctions de drag and drop notamment. [La page de documentation](https://help.gnome.org/users/gnome-terminal/stable/) sur le site [gnome.org](http://gnome.org) est très bien faite !
-   KDE propose l'émulateur **[Konsole](https://konsole.kde.org/)**, qui réécrit toutes les fonctionnalités de xterm, avec des ajouts assez intéressants comme, par exemple, son intégration native dans divers outils de développement tels que KDevelop, Kate, ou encore l'explorateur de fichier Dolphin.
-   **[xfce-terminal](https://docs.xfce.org/apps/terminal/start)** a été développé pour remplacer GNOME Terminal et propose les fonctionnalités essentielles, comme ses cousins mais sans dépendance à tel ou tel environnement de bureau (GNOME ou KDE par exemple). Il est donc très léger. Il est livré par défaut avec XFCE.
-   **[urxvt](https://sourceforge.net/projects/rxvt/)**, mon terminal préféré, malgré son nom un peu nerd... Ce programme est la suite logique de xterm épuré des fonctionnalités jugées non indispensables. Donc, c'est difficile de faire plus léger ! Outre le fait de pouvoir le lancer en arrière-plan en tant que démon (ou _daemon_) il propose également les fonctionnalités classiques : gestion des couleurs et des onglets lorsque nécessaire notamment.

## Comprendre les interactions entre terminaux et hyperviseurs de type 1 et 2
[[Virtualisation]]
L'installation d'un serveur Linux sur un hyperviseur de niveau 1 ne change rien. L'installer sur un hyperviseur de niveau 2 peut en revanche créer quelques ambiguïtés. En effet, l'hyperviseur de niveau 2 (dans l'exemple ci-dessous Oracle Virtualbox) va proposer l'affichage de la console et des terminaux physiques de manière virtuelle.

## Découvrir Shell
Programme exécuté lors de la connexion de l’administrateur sur un terminal.

Le rôle principal du shell est d'exécuter les commandes saisies par l'administrateur lui permettant d'effectuer des appels systèmes vers le noyau.Sous Linux, le shell standard est le **Bash** (pour Bourne Again Shell).

Bash est un programme écrit en C, visant à respecter au maximum [les standards POSIX](https://standards.ieee.org/standard/1003_1-2017.html) concernant les interpréteurs de commandes. Il est livré en standard sur la plupart des distributions Linux SystemV/d (Les distributions BSD implémentent plutôt C Shell par défaut), il est compatible avec “presque toutes les versions de Unix” et est disponible également pour [[Windows]] !

# Comprendre l’[[Arborescence Linux]]
La [fondation Linux](https://www.linuxfoundation.org/) est responsable du maintien de la norme définissant l’arborescence des systèmes Unix/Linux. Cette norme est appelée **[FHS** pour **Filesystem Hierarchy Standard** et est disponible sous plusieurs formats](http://refspecs.linuxfoundation.org/fhs.shtml).

Ce document recense
-   les répertoires identifiables proposant un usage clair et défini
-   indiquer la liste minimale des répertoires, sous répertoires et fichiers attendus pour chacun ([Liste minimale des répertoires directement sous la racine /](https://course.oc-static.com/courses/7274161/Liste+minimale+des+e%CC%81le%CC%81ments+sous+la+racine+%3A.pdf.pdf) )

Le respect de ce standard permet :
-   d’anticiper les répertoires contenant les informations recherchées, quelque soit la distribution
-   d’utiliser une arborescence commune et connue pour déployer, installer et configurer des programmes

Par exemple :
-   Les répertoires contenant des informations stockées sur un équipement mais utilisées par d'autres équipements seront identifiés par le mot-clé "**shareable**" (partageables en français). Par exemple, le répertoire **`/home`** contient traditionnellement les répertoires personnels des comptes utilisateurs du système, et ces données peuvent être partagées entre utilisateurs sur le même serveur, voire entre utilisateurs sur un serveur différent.
-   Les répertoires contenant des fichiers qui ne peuvent pas ou ne doivent pas être partagés entre plusieurs équipements seront marqués "**unshareable"** (non partageables en français). Nous pouvons citer ici **`/boot`** qui contient notamment le noyau Linux exploité sur l'équipement.
-   Les répertoires contenant des données qui ne peuvent pas changer d'elles-mêmes, ou sans l'intervention de l'administrateur, avec nécessité d'une élévation de privilèges sont marqués "**static"**. On peut à nouveau citer ici **`/boot`** bien entendu, mais également **`/etc`**, par exemple, qui contient traditionnellement les fichiers de configuration du système et des services.
-   Les répertoires qui ne sont pas marqués statiques sont marqués "**variable"** (variables). On peut retrouver ici le répertoire `/**home**` évidemment, mais également **`/var/www`** pour les sources d'un site web par exemple.

## Les principaux répertoires de l’arborescence

### /root
Ce répertoire est facultatif.
Exclusivement pour les tâches administratives du système.

### /home
Ce répertoire est facultatif.
Les fichiers de configuration nécessaires aux utilisateurs pour exploiter des programmes et applications doivent être stockés das un sous rpertoire de `/home` désigné par le login du compte utilisateur, préfixé d’un `.`

### /usr
Il contient des répertoires dans lesuels se situent des commandes :
-   **`/bin`**: ce sont les commandes critiques pour le bon fonctionnement du système, quel que soit son objectif. Elles sont lancées par le système et par l'administrateur ;
-   **`/sbin`**: ce sont les commandes uniquement à destination de l'administrateur pour la gestion du système.
-   **`/usr/bin`**: ce répertoire contient majoritairement les commandes à destination de tous les utilisateurs du système, privilégiés ou non.
-   **`/usr/sbin`**: ce sont des commandes à nouveau à destination unique de l'administrateur, mais non critiques pour le bon fonctionnement du système.
-   `/usr/local/bin` : contient tous les binaires compilés manuellement par l’administrateur après l’installation du système

D'un système à l'autre, les éléments contenus dans ce répertoire sont censés fonctionner exactement de la même manière.

### /var
Il stocke toutes les informations utilisateurs, administrateurs et systèmes variables.
Normalement, avec une utilisation classique de **`/var`**,**`/usr`** devrait pouvoir être utilisé en lecture seule ! Ce qui est un gage de sécurité très important.
Quelques sous-répertoires de `/var` :
-   **`/var/log`**: répertoire contenant l'arborescence de toutes les traces systèmes et applicatives. C'est dans ce répertoire qu'il est possible de consulter les traces des historiques de démarrage du système, de connexion des comptes utilisateurs, d'activité des services réseaux ([[SSH]], HTTPD, SMTP, etc.) ainsi que les traces du noyau. Généralement les applications installées sur le système disposent de leur propre sous-répertoire (**`/var/log/apache2`**par exemple).
-   **`/var/run`**: répertoire contenant toutes les données relatives aux processus en cours d'exécution, les sémaphores, les données applicatives, les fichiers numéro de processus, etc.
-   **`/var/spool`**: répertoire contenant des données stockées de manière temporaire entre processus. Souvent, ce répertoire est utilisé pour stocker des données relatives à des actions ou tâches à effectuer dans un futur proche par les processus en cours d'exécution.
-   **`/var/mail`**: c'est le répertoire de stockage des messageries électroniques locales des comptes utilisateurs du système.

## Les systèmes de fichiers virtuels
### /proc
Contient toutes les informations concernant le processus
-   `/proc/cpuinfo` contient les informations sur le processeur maintenu par le noyau
-   **`/proc/version`** contient la version exacte du noyau en exécution,
-   **`/proc/meminfo`**, les informations détaillés sur la mémoire vive gérée par le noyau,
-   **`/proc/uptime`**, le temps d'exécution cumulé,
-   **`/proc/cmdline`**, les paramètres passés au démarrage du noyau, etc.

**`/proc`** contient également beaucoup de répertoires, dont la grande majorité porte des noms à base de chiffres. En effet, tous les processus en exécution sur le système sont identifiés par un numéro unique géré par le noyau.

Ainsi ce dernier met à disposition les informations concernant chaque processus dans le répertoire portant son numéro associé.

# Visualisez des fichiers
## Les streams linux
Tous les programmes exécutés sous Linux disposent de 3 streams (= canaux) donnés :
1.  **`stdin`**(pour standard input) : c'est le canal de l'entrée standard, et par défaut, lorsque vous lancez une commande, c'est votre clavier. La commande sera éventuellement capable de lire les informations saisies avec le clavier via ce canal. Il porte le descripteur de fichier **numéro 0** ;
2.  **`stdout`**(pour standard output) : c'est le canal de la sortie standard, et lorsque vous lancez une commande depuis un terminal, c'est l'écran par défaut. Le résultat et les données affichées par la commande sont diffusés sur l'écran. Il porte le descripteur de fichier **numéro 1** ;
3.  **`stderr`**(pour standard error) : c'est le canal du flux concernant les erreurs, et par défaut, lorsque vous lancez une commande, c'est aussi l'écran. La commande va différencier les données “normales” des données “erreur” et peut changer de canal pour diffuser ces informations.

Pour manipuler ces canaux, il est nécessaire d'utiliser les caractères représentant des :
-   chevrons simples tels que**`>`**et**`<`**,
-   mais aussi doublés tels que**`>>`**et**`<<`**.

# Editez et supprimez des fichiers
## Emacs

[Sans titre](https://www.notion.so/84e684340f164e7d93c8d5766c060377)

[GNU Emacs Reference Card](https://studylib.net/doc/8133095/gnu-emacs-reference-card)

## Nano
Idéal lorsqu’on vient du monde de [[Windows]] :
-   les fonctionnalités d'édition sont classiques,
-   pas de distinction entre mode commande et mode saisie,
-   à l'ouverture de nano, vous êtes prêt à saisir,
-   et les touches de direction fonctionnent !

## Créer un fichier
```powershell
su - #passage en root
cd ./Documents #je me déplace là où je veux le créer
cat > [nom du fichier] #création du fichier
#j'appuie sur ENTREE
#je peux écrire directement dans le fichier
#j'enregistre avec CTRL + D
#je reviens à mes commandes avec CTRL + D
```

## Copiez, déplacez et supprimez des fichiers sous Linux
### Le fichier / l’inode
Un fichier est une structure de langage C définie directement au niveau du code noyau de Linux. On appelle cette structure inode.

Structure de l’inode (= fichier) :

### Blocs directs
Composé de 12 champs, ils contiennent les adresses directes des données du fichier sur le périphérique de type blocs les contenant ([[Disque dur]], clé USB ...)

### Blocs indirects
Ces champs contiennent les pointeurs vers d’autres inodes dont la totalité des champs est adressée pour des blocs de données.

Toutes ces différentes vues sont des niveaux de zoom sur un même fichier, qui va grossir au fur et à mesure qu’on va loin dans les redirections. En gros :

### Copier un fichier

```powershell
cp [nom du fichier copié] [nom du fichier créé]
```
Mon [nom du fichier créé] est donc une copie de mon fichier de base, il apparait dans le même dossier.

# Configurez les cartes réseaux
## Configurez le nom du réseau de mon serveur
Le system hostname sert d’identifiant par défaut de ma machine.
1.  le fichier**`/proc/sys/kernel/hostname`** contient la valeur courante du nom réseau du serveur,
2.  la commande **`hostnamectl`** permet de la modifier,
3.  le fichier**`/etc/hostname`** permet d’initialiser le nom réseau au démarrage.

> il est de coutume de garder le nom sous un format très simple, le plus souvent un mot, représentant un champ lexical commun entre plusieurs serveurs. (étoiles, nom de personnages, nom de villes ...)

## Détectez les interfaces réseaux de mon système
1.  la commande **`dmesg`** pour essayer de détecter les cartes réseaux reconnues par le noyau lors du démarrage,
2.  consulter le système de fichier virtuel**`/sys`** pour lister les interfaces réseaux,
3.  constater une évolution liée à **`Systemd`** dans le nommage par défaut de ces interfaces.

## Configurez les cartes réseaux de manière dynamique
Sur toutes les distributions Linux, vous pouvez configurer de manière dynamique les cartes réseaux avec la commande **`ip`**.

Toutes les configurations de réseau sur les cartes gérées par la commande **`ip`** sont dynamiques. Elles seront donc perdues entre chaque "reboot" du serveur.

Pour configurer de manière statique les cartes réseaux de Linux, il est nécessaire de saisir les informations dans des fichiers de configuration qui vont être lus pendant le boot du serveur.

### sous les distributions dérivées **DEBIAN**
Sous Debian et ses dérivés, le répertoire de configuration des interfaces réseaux est**`/etc/network`**. Le fichier **interfaces** permet de déclarer cette configuration de manière statique.

### sous les distributions dérivées **REDHAT**
Pour les distributions REDHAT et dérivés (notamment CentOS), le répertoire de configuration des cartes est **`/etc/sysconfig/network-scripts/`**. Ce répertoire contient notamment un fichier préfixé **`ifcfg-`** pour chaque carte reconnue par le système.

la commande **`systemctl`** permet de prendre en compte ces configurations en redémarrant le service réseau.