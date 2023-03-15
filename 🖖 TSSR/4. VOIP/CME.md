= Cisco Call Manager Express

# Généralités

Pour installer Packet Tracer : [lab-downloads](https://skillsforall.com/resources/lab-downloads)

CME est une solution de traitement des appels intégrée à certain routeurs d'accès Cisco sous la forme d'un ensemble de fonctionnalités.
Protocole : SCCP ou SIP
Port 2000

# Configuration

Je me connecte à Packet Tracer pour configurer cette solution sur un [[Routeur]] 2811. 
Je vais avoir besoin de plusieurs éléments : 
- DHCP : gestion du network, default [[Routeur]] (définit la passerelle, le Proxy SIP via option 150 pour faire passer les flux de voix).
- dial numbers : gestion des extensions
- max phones : nombre maximum de téléphones sur le réseau
- MAC : attribuer un téléphone à un numéro en s'appuyant sur l'adresse MAC
- button : gestion de la sonnerie
- type : IP phone ou Softphone

Reproduire ce schéma dans Packet Tracer : 

![[Pasted image 20221116113124.png]]




 

  

Avec l’outil texte         nommer/étiqueter les différents matériels comme ci-dessous :

Il existe 3 modes avec le système Cisco

-        Le premier de ces modes est le mode dit « **Utilisateur ou Invité** ». C’est un mode de supervision, il vous permet d’effectuer des pings et quelques show (c’est une commande qui sert à afficher des renseignements sur le matériel) `“Nom du Router>”` s’affiche quand vous êtes dans ce mode. À partir de ce mode, on peut passer en mode **Privilège grâce à la commande enable.**

-        Le deuxième est le mode « **Privilège** ». Vous pouvez le voir comme l’équivalent du mode root chez Linux, on le reconnaît grâce au **#** dans le prompt. Il vous permet d’effectuer les mêmes commandes que le mode Utilisateur (avec tous les show) et de gérer les fichiers à l’intérieur du [[Routeur]] (copy, erase).

`“Nom du Router#”` s’affiche après le nom du [[Routeur]] quand on est dans ce mode. De ce mode, **on peut passer en mode « Configuration Globale » avec la commande** _configure terminal_.

-        **Le troisième est le mode « Configuration globale »** : seul mode où on peut administrer

**If** : sous mode de configuration globale, permet les administrations des interfaces ou des services.

Pour sortir d’un mode, on fait : **exit**

Pour exécuter une commande qui se trouve dans un autre mode : **do + commande**

Faire la commande suivante pour éviter les recherches DNS :

CME (config)# **no ip domain-lookup**

Entrer les exclusions des machines déjà installées

CME (config)#  **ip dhcp excluded-address 192.168.150.1**          (router)

On crée un pool d’adresses dont le nom est Voice

CME (config)# **ip dhcp pool Voice**

CME (dhcp-config)#

Pour déclarer le réseau

CME (dhcp-config)#**network  192.168.150.0  255.255.255.0**

On déclare la passerelle

 CME (dhcp-config)#**default-router  192.168.150.1**

On déclare les options

CME (dhcp-config)#**option 150 ip 192.168.150.1**

_On déclare le serveur VOIP (ici le [[Routeur]] fait office de VOIP, donc on prend son IP)_

_Option 150 pour la VOIP (on peut définir de 0 à 254 en fonction du type de [[Routeur]]) (la commande « option » est exclusivement pour la VOIP)_

On donne le nom de domaine : espace de nom qui permet de regrouper tous les éléments (objets) d’un réseau au sein d’un seul et même emplacement physique.

CME (dhcp-config)#domain-name tssr.lan

On déclare le DNS : DNS-server 192.168.140.4

Cisco Jabber : application Cisco qui permet d’utiliser les CME et tous les services de communication unifiée (VoIP, IM, VideoCall, Transfert de Fichiers, etc.)

Fin de configuration DHCP**.**

**Configurer les pc**

Cliquer sur l’icône téléphone puis sur l’onglet « **desktop »** et « **IP configuration »**, cocher « **DHCP** ». (A faire pour les 2 pc)

  

Toujours sur « **pc** », « **onglet desktop** », cliquez sur command **« prompt** « et faire un ping de l’autre pc.

Pour faire sauvegarder la configuration

CME (config)#**do write**

Building configuration….

[OK]

**Configuration des téléphones**

CME (config)#**telephony-service**

Définir le nombre maximum de téléphones fixes

CME (config-telephony)#**max-ephones 4** 

Définir le nombre de numéros de téléphones

CME (config-telephony)#**max-dn 4**

Pour déclarer qui sera notre serveur SIP

CME (config-telephony)#**ip source-address 192.168.150.1 port 2000**

Assigner automatiquement 4 numéros

CME (config-telephony)#**auto assign 1 to 4**         

Pour déclarer le téléphone 1

CME (config-telephony)#**ephone-dn 1**  

Définir un le numéro du téléphone 1

CME (config-ephone-dn)#**number 101**  

Pour déclarer le téléphone 2

CME (config-telephony)#**ephone-dn 2**  

Définir un le numéro du téléphone 2

CME (config-ephone-dn)#**number 102**  

Refaire pour les autres téléphones :

**ephone-dn 3**

**number 11**   

**ephone-dn 4**

**number 12**   

Faire « **exit** » et se reconnecter à ephone 1 pour configurer le soft phone.

CME (config-ephone-dn)#**ephone 1**

CME (config-ephone)#**type 7960 (IP Phone)**

Faire la même chose pour le téléphone 2.

Pour les softphones Cisco utiliser le type **:  CIPC (Cisco jabber)**

Ensuite cliquer sur l’icône du téléphone, et enlever le câble et le remettre pour la prise en compte de la nouvelle configuration, puis faire un test d’appel sur les téléphones.

**Show running-config** : pour voir la configuration et la copier si possible pour une future configuration.