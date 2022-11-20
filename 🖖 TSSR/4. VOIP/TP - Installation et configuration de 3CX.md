
Logiciel libre 
Système de communication unifié qui peut gérer l’ensemble des besoins de communication d’une entreprise. 

Fonctionnalités :
- Enregistrement des appels
- Identification de l'appelant
- Possibilité de faire de la visiophonie
- Votre messagerie vocale disponible sur votre adresse e-mail
- Un panneau de commande simple et intuitif accessible depuis une interface web
- Possibilité de créer des centres de conférences
- Serveur de messagerie instantanée (Openfire) intégré
- Serveur de mail incluant le support "multi-domaine"
- Arrêt de votre serveur à partir du web
- Sauvegardes sur un serveur FTP, restauration et sauvegarde automatique
- Envoi de documents digitales vers des numéros de fax à travers une imprimante virtuelle
- Centralisation des mises à jour via un gestionnaire
- Configuration graphique des paramètres
- Visualisez le rapport de l'utilisation des ressources
- Visualisez les rapports des appels entrants/sortants et de l'utilisation des canaux
- Module de messagerie vocale intégré
- Aide disponible en ligne
- Modules supplémentaires carte d'appels et SugarCRM inclus
- Présence du module Flash Operator

# Installation
Téléchargement ISO 3CX
[Installation 3CX](https://www.3cx.fr/docs/manuel/installation-debian-linux-ipbx/)

Choisir la version 3CX xx
Enter option : 1
Se connecter avec un navigateur : http://192.168.171.133:5015?v=2

Puis, [configurer le PBX](https://www.3cx.fr/docs/manuel/configurer-votre-pbx/)




## Configuration de l’accès distant sur Elastix

Si vous voulez vous connecter au serveur via ssh ou bien directement sur cette console utiliser comme login **root** et comme password votre mot de passe pour l’utilisateur root (le premier mot de passe que nous avons saisi durant l’installation).  Une fois vos informations de connections indiquées, vous verrez apparaitre la page suivante :

Bon maintenant, il faut connecter votre serveur à votre réseau et vous connecter sur un autre PC du réseau (bien sûr, il faut que votre Serveur Elastix soit allumé et que les 2 PC puissent communiquer).

Maintenant à partir d’un autre PC connecté au même réseau essayé de faire un Ping sur l’adresse du serveur qui dans notre cas est 192.168.255.254 (ce n’est pas obligatoire, mais c’est utile pour teste si les 2 machines sont bien en réseau).

Si le Ping ne passe pas ? Vérifier bien votre connectique.

Enfin, le Ping passe. Ouvrez un navigateur sur le deuxième ordinateur (celui sur lequel vous avez fait le Ping vers le serveur). Taper l’adresse du serveur dans le **navigateur Internet Explorer** « [http://192.168.255.2](http://192.168.255.20)**54** »et valider vous verrez une page vous indiquant que le certificat de votre serveur n’est pas valide cette page change en fonction de votre navigateur et de sa version.

Cliquer sur « **Informations** » et ensuite sur « **Accéder à la page web (non recommandé)** » :

Ce n’est pas dangereux de le faire, car nous nous connectons à notre serveur personnel se message est dû au fait que le certificat que vous avec dans votre serveur n’est pas reconnue par Chrome.

Vous pourrez plus tard si vous le voulez avoir un certificat reconnu (aucun intérêt si ce serveur est juste destiné à être utilisé dans l’entreprise).

## Configuration d’Elastix

Très bien, parvenu à ce niveau, après avoir cliqué sur « **Continuer vers le site** », vous verrez la page ci-dessous. Le nom d’utilisateur c’est **« admin »** et le mot de passe c’est celui que vous avez spécifié lors de l’installation (le dernier mot de passe crée durant l’installation). Cliquez ensuite sur le bouton « **Submit »**.

**_NB_** _: Si un jour il vous arrive d’oublier votre mot de passe de l’administrateur Web ou alors celui de la base de données, il vous suffira de vous connecter en tant que root et de taper la commande_ :

**elastix-admin-passwords –change**

Ensuite un assistant vous demandera de rentrer un nouveau mot de passe pour la base de données et pour l’administrateur Web.

Une fois connectée, vous verrez, une interface similaire à celui-là :

Cliquez sur l’onglet « **Préférences »**et ensuite choisissez la langue qui vous convient le mieux. Pour finir cliquer sur « **Save »**.

  

La création d’un utilisateur est importante pour éviter d’utiliser le compte admin par défaut. Nous allons donc créer un utilisateur et lui donner les mêmes droits que l’admin.

Cliquez sur « **Système »** et ensuite sur « **Utilisateurs »**.

Dans la fenêtre, cliquez sur « **Créer un nouvel utilisateur »** et remplissez les champs comme sur l’image.

**_N.B_** _: Les groupe Operator et Extension sont des groupes spécifiques pour la supervision et la gestion du serveur Elastix. Les utilisateurs de ses groupes seront limités à des taches uniques sur le serveur_.

  

Vous pouvez également modifier les paramètres IP dans l’onglet « **Réseau »** en cliquant sur « **Editer** ». Les paramètres réseau modifiable sont le nom **Hôte**, la **Passerelle** et les **DNS**.

Pour modifier les paramètres TCP/IP de la carte réseau ou des cartes réseau du serveur, cliquez sur « **Ethernet 0 »**, ensuite vous pourrez modifier l’**Adresse IP** ainsi que le **Masque** ou mettre la carte en **DHCP**.

L’envoi des emails est également possible avec Elastix car il est doté d’un serveur de mail intégré Postfix qui va s’appuyer sur le SMTP pour l’envoie des mails sur un ou plusieurs domaines.

Cliquez sur l’onglet « **Email »**, puis sur « **Domaines »**, vous devez ajouter un nouveau domaine en cliquant sur « **Créer un domaine »** et entrer le nom de votre domaine **« tssr.info »** puis cliquez sur « **Sauver »**.

  

Une fois votre domaine créer il apparaitra dans la « **Liste Domaine »**.

Il faut maintenant créer les comptes email pour transférer les appels manqués des utilisateurs pour qu’il puisse avoir une boite vocal liée à leur adresse email. Ainsi ils pourront être notifier par mail lorsqu’ils rateront un appel téléphonique.

Cliquez sur « **Comptes »** puis sélectionner votre domaine « **tssr.info »** et cliquez sur « **Créer un compte »**.

Vous pouvez ainsi visualiser la liste des comptes

  

Nous devons maintenant accéder aux boites mails créer en cliquant sur « **Webmail »**. Elastix intègre un client de messagerie roundcube qui nous donne la possibilité d’ouvrir notre boite mail directement depuis le serveur Elastix. Entrant les informations de l’utilisateur par exemple pour Ghislain nous allons mettre comme utilisateur : « [ghislain@tssr.info](mailto:ghislain@tssr.info) **»** et le mot de passe : « **P@ssw0rd »** (qui est celui qui a été défini lors de la création du compte), puis cliquez sur « **Authentification »**.

Ainsi vous avez l’accès à votre boite mail. Elle peut également servir pour l’envoi des mails en interne et en externe si d’autre domaine sont configuré.

  

Maintenant nous allons configures des numéros SIP pour les utilisateurs. Cliquer sur l’onglet **« PBX »**. Rassurez-vous que « **périphérique SIP »** soit sélectionné et cliquer sur « **Soumettre »**.

Nous devons savoir que le compte SIP désigne un numéro de téléphone qui sera attribué à un utilisateur pour qu’il puisse être joignable par téléphone.

Vous verrez ensuite une page avec beaucoup de champ à remplir. Il n’est pas nécessaire de remplir tous les champs sauf dans le cas où nous voulons apporter plus d’options sur à l’extension.

Sur la partie « **Ajout Extension »,** remplir les éléments suivants :

**Extension Utilisateur**

**Nom affiché (CID)**

  

Dans les « **Options Extension »**, laisser par défaut car nous ne voulons rien modifier spécifiquement.

Dans les « **Options Périphériques »**, remplissez le champ « **secret »** en indiquant le mot de passe de connexion de l’utilisateur SIP. Dans notre cas, ce sera « **P@ssw0rd069 »**

Dans les « **SDA/CID »** associé, nous n’allons rien mettre car nous n’avons pas de télécopieur.

Dans « **Boite vocale »**, « **Activer »** la boite vocale et indiquer un mot de passe pour la boite vocale (en chiffre) nous avons choisi **123456789** ainsi que l’email (facultatif c’est pour recevoir les messages vocaux le cas échéant) « [tssr@tssr.info](mailto:tssr@tssr.info) **»**.

« **Options Extension** » : Laissez sur « **Use State** »

« **Language** » : Le code de la langue (le code a deux chiffres).

_Ex : **fr** pour français, **en** pour anglais._

  

« **Option d’enregistrement** » : Laissez par défaut.

« **Services de Dictée** » : Laissez par défaut.

« **Locater Vmx** » : Laissez par défaut.

  

« **Optionnal Destinations** » : Laissez par défaut et cliquez sur le bouton « **Soumettre ».**

Nous avons fini de configurer notre compte SIP sur le serveur. Maintenant nous allons passer à la configuration de notre Client qui utilisera le protocole SIP pour passer des appels.

Avant de quitter la page de configuration SIP cliquez sur **Apply Config** au-dessus de la page.

Répétez l’opération pour les utilisateurs **Ghislain<065>, Benoit<066>, Aina<067>, Sayere<068>.**

## Configuration du Client

Les clients VoIP sont nombreux et peuvent être soit physique soit logique. Lorsqu’ils sont physiques, nous parlons de IP phone c’est-à-dire des téléphones qui sont connecter au réseau IP. _Par exemple les Cisco System CP-7940G, etc_. Lorsqu’ils sont logiques, c’est une application de type, _Jitsi,_ _X-lite,_ [_Ekiga_](http://www.ekiga.org/)_,_ [_,_](https://jitsi.org/Main/Download) _3CX, Zoiter, etc_. Ils prennent en compte le protocole SIP et transforme votre ordinateur, tablette ou smartphone en téléphone.

Dans notre cas, nous allons installer des softphones 3CXPhone5 et Jitsi afin de tester votre PBX Elastix.

Télécharger les applications sur le web et installer les sur le ou les postes clients.

  

Si vous rencontrez ce message lors de installation de **3CXphone5**, c’est que vous n’êtes pas administrateur de votre pc client.

Pour résoudre ce problème, saisir « **gestion de l’ordinateur »** dans la barre de recherche de Windows.

Dépliez « **utilisateurs et groupe locaux** » puis cliquez sur le dossier « **utilisateurs** » et double-cliquez sur « **Administrateur ».**

Décochez « **le compte est désactivé »** puis cliquez sur “**OK».**

Faire clic droit sur « **Administrateur »** et cliquez sur « **Définir le mot de passe …**». Sur la fenêtre qui apparait, cliquez sur « **Continuer »**. Saisisez le mot de passe et la confirmation du mot de passe du compte administrateur et cliquez sur « **OK** ».

Connectez vous ensuite avec le compte administrateur et le mot de passe précedemment saisi.

Maintenant, vous pouvez installer 3CXPhone5. (_réinstaller les tools si besoin_)

## Configuration du softphone

Exécuter **3CXPhone**, cliquez sur « **Set accounts »**, puis dans la fenêtre cliquez sur « **New »**. Remplissez les champs comme sur l’image.

_Remarque: Dans le champ « **Password»** vous devez saisir le password du profil ghislain de Elastix. Dans la champ « **I am in the office – local IP** », saisir l’adresse IP du serveur Elastix_

Validez ensuite vos modifications en cliquant sur « **OK ».**

Le compte apparait maintenant dans la liste des comptes SIP.

Vous pouvez éventuellement supprimer le compte inutilisé **New** account en le sélectionnant et en cliquant sur « **Remove »**.

Valider le compte en cliquant sur « **OK »**. Le 3CXPhone s’enregistrera alors automatique sur le serveur PBX et vous verrez apparaitre « **Available »**. Votre connexion est réussite. 

Faite de même avec le deuxième client 3CXPhone de la deuxième machine virtuelle **PC01** et connecter le **compte SIP 069 de tssr**.

               3CXPhone PC02                                                           3CXPhone PC02

  

## Test d’appel

Pour tester les appels entre Ghislain et TSSR, composez le numéro de votre correspond TSSR<069> depuis le softphone Ghislain.

  

Vous pouvez ainsi communiquer avec votre correspondant.

## Accès à la boite vocale

Lorsqu’un utilisateur manque un appel, si la boite vocale est configurée ce qui est notre cas, nous pouvez écouter les messages vocaux en se connectant au lien suivant : [https://192.168.255.254/recordings](https://192.168.255.254/recordings) et remplissez les identifiants par le numéro de compte à savoir **<069>** pour tssr et son mot de passe **123456789** comme sur l’image.

Nous sommes maintenant connectés dans la boîte vocale de tssr<069> et pouvons désormais écouter les messages vocaux.

  

Nous allons maintenant rappeler **tssr** et laisser un message vocal. Puis actualisez la boîte de messagerie. Vous verrez apparaitre le nouveau message vocal. Pouvez ainsi le lire , le télécharger  ou appeler votre boite vocale  pour écouter le message.

## Transfert d’appel

Le transfert d'appel vous permet de rediriger vos appels vers un autre numéro de téléphone. Vous pouvez effectuer cette action directement depuis le téléphone. Vous pouvez également effectuer cette action depuis votre serveur PBX.

Transfert d’appel depuis le serveur PBX

Dans l’onglet « **PBX »**, cliquez sur « **Suivez-Moi »**, choisissez l’extension « **Ghislain<065> »**, dans « **Editer Suivez-moi »**, modifier « **Liste Suivez-moi »** et ajouter l’extension de l’utilisateur qui doit recevoir les appels de Ghislain lorsqu’il est absent « **tssr<069> »** et laissez les autres paramètres par défaut.

Dans « **Destination si pas de réponse »**, déroulez la liste et sélectionner Extensions puis choisissez l’extension « **<069>tssr »** où doit être transférer les appels de Ghislain<065>.

Cliquez sur « **Appliquer les Modifications »** pour valider les configurations apportées.

Nous devons maintenant configurer un second softphone sur Jitsi et y connecter le compte **benoit<066>**.

Lancez Jitsi sur le poste où est connecté l’utilisateur **tssr<069>** et configurer l’application comme sur l’image en cliquant sur « **Option »** puis « **Compte »**, cliquer sur « **Avancé** » puis ajouter le **Nom affiché** « **Benoit** », puis cliquez sur **Suivant** et ensuite **S’identifier**.

Vous êtes maintenant connecté avec l’utilisateur Benoit<066>.

Lancer l’appel vers Ghislain en composant son numéro depuis Jitsi et l’appel sera transférer vers le softphone **tssr<069>** comme dans l’image.

**Voilà le transfert d’appel fonctionne**.  
