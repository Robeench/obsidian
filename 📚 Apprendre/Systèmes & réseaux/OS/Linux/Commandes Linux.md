
# Commandes [[Linux]]
`apt` pour advanced package tool, utilitaire présent sur les distributions debian. Permet d'installer, supprimer un logiciel ou encore mettre à jour ce dernier ou mettre à jour ma distribution [[Linux]].
	`apt update` pour trouver la dernière version d’un logiciel
	`apt upgrade` pour mettre à jour un logiciel
	`apt search [nom du logiciel]` pour trouver le nom d’un logiciel dans la bibliothèque des logiciels disponibles
	`apt install [nom du logiciel]`pour installer le logiciel
	`apt purge [nom du logiciel]` pour supprimer un logiciel
`CTRL + C` pour arrêter le `ping`
`CTRL + R` pour rechercher dans mon historique de commandes un mot spécifique
`clear` efface mon terminal
`cat [chemin du fichier]` pour catenate, permet de prendre un ou plusieurs flux de données en paramètre d’entrée et de les afficher à l’écran sur le terminal.
`cd [chemin du répertoire]` pour change directory permet de se déplacer dans l’arborescence
`df` pour disk free, pour afficher des informations relatives aux systèmes de fichiers sur l’espace total et l’espace disponible.
`dpkg` pour debian package, logiciel formant la base de bas niveau du système de gestion de paquets Debian. Utilisable pour installer, configurer, mettre à niveau ou supprimer des packages Debian et récupérer des informations sur ces packages Debian.
`dmesg` détecte les cartes réseaux reconnues par le noyau lors du démarrage
`echo` pour afficher un message ou afficher le résultat d’autres commandes
`file [chemin du fichier]` permet de récupérer des informations sur un fichier
`file [chemin du fichier/*]` permet de lister l’ensemble du répertoire
`grep [mot recherché] [chemin du fichier]` permet de filtrer le flux de données selon un pattern
`help` affiche le nom des commandes internes
`help [nom de commande interne]` permet d’avoir plus d’informations sur ces options et caractères disponibles
`[nom de commande externe] --help` permet d’avoir plus d’informations sur ces options et caractères disponibles
`history` affiche l’historique des commandes passées sur mon terminal
	`![numéro de la commande dans l'history]` pour l’appeler
`ip a` permet de configurer de manière dynamique mes cartes réseaux
`id` permet de relever les informations concernant le compte utilisateur connecté
`less` affiche les données passées en paramètre, paginées directement sur le terminal.
	`ESPACE` pour passer à la page suivante
	`b` pour revenir à la page précédente
	`-N` affiche les lignes du fichier
	`G` dernière ligne du fichier
	`g` première ligne du fichier
	`/[mot recherché]` permet de faire la recherche d’un terme
`ls` affiche le contenu d’un répertoire
`lsblk` indique la manière dont sont connectés mes périphériques de stockage
`man [nom de commande externe]` permet d’accéder au manuel unix concernant cette commande
`mkdir [nom de répertoire à créer]` permet de créer un répertoire
`nano` permet d’éditer du texte
	`nano /etc/network/interfaces` permet de modifier les interfaces réseaux
`ping` pour packet internet groper, permet grâce à l’envoi de paquets de vérifier si une machine distante répond et donc si ell e est accessible par le réseau.
`pwd` me dit où je me trouve dans la machine
`reboot` pour redémarrer le système
`route -n` accéder à la table de routage
`sed` pour stream editor, utilise les expressions régulières pour transformer un flux de données à la volée de manière non interactive
`su` (switch user) permet de changer d’utilisateur pour root (je reste au même endroit)
`su nomdutilisateur` permet de changer d’utilisateur pour celui indiqué
`su -` permet d’être en home root
`type [nom de commande]` permet de récupérer des informations concernant une commande

# Options
Il est possible de cumuler les options sous la forme `ls -ltr` au lieu de `ls -l -t -r`

`-a` permet d’afficher les fichiers cachés
`-h` pour human readable me traduit le volume des fichiers sous un format compréhensible
`-i` annule le key sensitive
`-l` liste le contenu avec les informations sous forme longue
`-n` affiche le numéro des lignes
`-o` isole un pattern
`-r` inverse l’ordre d’affichage
`-R` affiche tout le contenu de l’arborescence (R pour récursive)
`-t` tri dans l’ordre de modification le plus récent

# Opérateurs
`&&` permet de cumuler des commandes entre elles

# Variables
`$PS1` affiche les informations du prompt (plus d’infos sur ces codes via : [change-bash-prompt-variable-ps1/](https://linoxide.com/change-bash-prompt-variable-ps1/))
`$SHELL` affiche le nom du shell (nom de la commande lancée après l’authentification)
`$PATH` liste de répertoires dans lesquels sont rangés des commandes que je vais rechercher automatiquement

# Divers
## Les différents types de commande [[Linux]]
### Commandes internes
Ces commandes sont livrées avec l'interpréteur de commandes directement, comme une primitive du shell. Elles sont disponibles à tout moment par l'administrateur du système. Cependant, il est probable que toutes ne soient pas forcément intégrées à l’interpréteur de commandes que vous allez utiliser. Il est également possible que leurs options ne soient pas toutes identiques non plus.

### Commandes externes
Ces commandes sont externes à l'interpréteur de commandes, c'est-à-dire qu'elles ne sont pas fournies par le shell. Elles sont généralement présentes sur le système sous la forme d'un fichier compilé binaire ou d'un fichier disposant des droits d'exécution (comme un script Perl par exemple).

#### Options et arguments
L’argument est pris en compte comme une entrée pour exécuter la commande.
L’option modifie la manière dont sort le résultat.

## Evolution en [[Routeur]]
`echo 1 > /proc/sys/net/ipv4/ip_forward` me permet de recevoir des paquets qui ne me sont pas destinés ([[Routeur]])
```shell
auto eth0:1
allow-hotplug eth0:1
iface eth0:1 inet static
  address 192.168.1.248
  netmask 255.255.255.0
  gateway 192.168.1.254
```

## Installation de logiciels
Si je télécharge un fichier .deb sur le site de l’éditeur :

```bash
cd Téléchargements/
ls
dpkg -i [nom du package]
```

Certaines dépendances peuvent ne pas être installés, il faut les installer pour que l’installation complète puisse se faire.
Si je télécharge un fichier .run (équivalent d’un fichier exécutable sous [[Windows]]). Il faut que je lui donne des droits d’exécution sinon il ne pourra pas être utilisé :

```shell
cd Téléchargements/
ls
chmod +x [nom du fichier]
./[nom du fichier]
```

--- 

modifier `dhcp` en `static`
`address 1.1.1.1`
`netmask 255.0.0.0`
`gateway 1.1.1.255`
pour définir une adresse [[IP]] précise
