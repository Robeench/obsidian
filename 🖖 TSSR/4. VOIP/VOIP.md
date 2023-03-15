[VOIP - Wikipedia](https://fr.wikipedia.org/wiki/Voix_sur_IP)
= Voice Over Internet Protocol

Permet de faire transiter sur le réseau [[IP]] ce que l'on peut appeler les flux multimédias : audio, vidéo et messages. 

# QoS
= Qualité de service
ensemble de techniques et de configuration à prendre en compte lors de la mise en place d’un service pour assurer une rentabilité optimale et de qualité.

## Délais perceptibles et variation du délai
L’écho ne doit pas être à plus de 100ms environ, si le délai maximum dépasse 100ms alors la communication sera dégradée et les interlocuteurs auront une communication décalée.

## Le taux d’erreur
Détection automatique des erreurs. 
Il doit être inférieur à 1.

## La bande passante
Le calcul de la bande passante dépend du codec (la façon ou format dont la voix sera codée avant d’être transmise) utilisé, du nombre de communications maximum et le débit de communication du [[Protocole]] de VOIP utilisé. 
Plus la bande passante sera élevée, plus la communication sera claire.

# Les facteurs du délai

## Solution de facture de délai

### Cas du réseau local
- Il faut utiliser des réseaux séparés (une box dédiée pour Internet, une autre box pour la VOIP…)
- Les réseaux peuvent être séparés de façon physique ou virtuel (VLAN)
- Dans le cas d’un réseau sans fils, il faut s’assurer d’utiliser des privilèges, des solutions gratifiantes (on va privilégier les **QoS)**.

### Choix du fournisseur
Pour bien choisir un fournisseur d’accès, nous devons contrôler les éléments suivants :
-        Le **[[SLA]]** (Service Level Agreement) qui est un contrat ou la partie d'un contrat par lequel un prestataire s'engage à fournir un ensemble de services à un ou plusieurs clients. Autrement dit, il s'agit d'une clause contractuelle qui définit les objectifs précis et le niveau de service qu'est en droit d'attendre un client de la part du prestataire signataire.
-        Une meilleure fiabilité
-        Un service complet
-        Avoir des lignes de backup
-        Réservation des priorités de trafic (ToS)

### Cas du réseau global
Dans la sélection de notre fournisseur, lorsqu’il s’agit d’un cas général, nous devons regarder les éléments suivants :
-        La dépendance égale avec d’autres fournisseurs (avoir plusieurs fournisseurs)
-        Best effort : avoir tous les moyens pour avoir les meilleurs résultats
-        TOS (Type Of Service) c’est la priorisation du trafic afin de rendre un trafic prioritaire.
-        DiffServ permet le contrôle des flux afin de définir quel trafic est prioritaire

# Protocoles
- H323
- [[SIP]] (Session Initiation Protocol) - Port 5060
- IAX – Inter Asterisk eXchange (Asterisk)
- MGCP – Media Gateway Control Protocol - Port 2427
- SCCP - Skinny Client Control Protocol - Port 2000
- RAS (Registration, Admission and Status) 
- RTP - Real-time Transport Protocol
- RTCP - Real-time Transport Control Protocol

Il existe des protocoles secondaires utiles et obligatoires tels que :
- [[DHCP]]
- TFTP pour la configuration et la mise à jour
- [[DNS]] pour les services d’annuaire et de localisation
- [[HTTP]] et [[HTTPS]] pour l’administration

Ces protocoles permettent de faciliter l’accès et l’administration du serveur VOIP via le réseau.

## Fonctionnement et structure des protocoles

### H323
Etablissement des connexions VOIP en point to point, entre 2 terminaux, avec l’envoi de son et de vidéo en temps réel et effectue de la vidéo-conférence, en s’appuyant essentiellement sur une connexion TCP via le [[Port]] 1720.

#### Schéma d'initialisation - Appel H323
1ère connexion : établissement de l’appel
2ème connexion : envoi des messages e-contrôle des flux médias et échange de capacité entre terminaux

### SCCP
= Skinny Client Control Protocol
Protocole propriétaire Cisco fonctionnant à peu près comme le H323, mais est plus léger et demande moins de ressources
- utilisation de la bande passante moindre
- peut gérer des conférences
- peut être utiliser entre l’IP et le softphone

Port 2000 

Peut être utilisé pour un petit réseau. Lorsque nous configurons une plateforme de VOIP selon Cisco, on parle de [[CME]] (Cisco Management Express), qui est le nom d’appellation d’une plateforme de VOIP de chez Cisco. 
Il est également connu sous le nom de Callmanager. Le softphone (client VOIP applicatif) permet à un utilisateur de téléphoner via un système de type Android, [[Windows]] ou Mac afin de passer des appels. 
Cisco Jabber est l’application propriétaire de chez Cisco pour les plateformes [[CME]].

### [[SIP]] 
= Session Initiation Protocol

Basé sur l’initiation de session lié à des comptes utilisateurs.
Il s'appuie sur 3 éléments :
- User Agent : génère un compte utilisateur associé à un utilisateur. Il est principalement utilisé sur des IP Phones ou Softphone
- Registrar : correspond au serveur qui permet d’authentifier les agents et les stocker dans une base de données. 
- Proxy SIP : fait office de passerelle pour les User Agent afin de contacter le serveur SIP. Toutes personnes voulant communiquer avec un autre user agent est obligé de passer par le proxy SIP.

#### Failles et attaques

##### Attaques DOS via requêtes BYE
Dans ce type d’attaque, le pirate va écouter le réseau afin de récupérer un message de requête soit du type REGISTER, soit du type INVITE et modifie certains champs contenus dans l’en-tête avant d’envoyer ce faux message de requête. L’appelé pense qu’il parle à un utilisateur spécifique alors qu’il parle au pirate. Ainsi, la victime ne pourra plus enregistrer son téléphone comme étant une adresse de contact convenable et tous les appels pour la victime seront redirigés vers le pirate.

##### Appel SPAM
Cette attaque a pour but de jouer un message préenregistré à la personne décrochant le combiné. Ce type de spam est défini comme étant une série d’essais d’initiation de session, essayant d’établir une session de communication vocal. Quand l’appelant décroche le combiné, l’attaquant relais son message à travers le média en temps réel.

##### Vol d’identité et détournement d’inscription
En règle générale l’inscription sur un serveur SIP nécessite un login et MDP. L’ensemble des messages SIP ne sont pas cryptés, si une personne malveillante aspire les processus d’authentification, elle peut utiliser une combinaison nom utilisateur/mdp pour être authentifié par le serveur. 
Une telle attaque n’est plus possible avec les dernières implémentations de la VOIP.

##### Inondation du serveur Proxy
Cette attaque a pour but d’inonder les serveurs proxy avec des messages INVITE. Le pirate envoie un gros volume de messages au proxy, qui doit les transférer vers le destinataire.
Le nombre de sessions concurrentes supportées est limité, les ressources sont rapidement épuisées, ce qui a pour conséquence que les appels passés par des utilisateurs légitimes utilisent le proxy victime.

##### Détournement d’appel à l’aide du serveur registrar
Cette attaque a pour but de détourner un appel en altérant les liaisons du serveur registrar, cad un serveur pirate se fait passer pour notre serveur légitime.

##### Débordement de la table des enregistrements
Cette attaque a pour but de provoquer un débordement de la table des enregistrements afin d’empêcher les utilisateurs de s’enregistrer sur le serveur registrar.

### RTP et RTCP

#### RTP
= Real Time Protocol
protocole qui permet principalement le transfert des données du serveur au(x) client(s) en temps réel. Il s’appuie sur le protocole TCP et UDP. La différence est que l’un fait la vérification avant appel (TCP) et l’autre non (UDP).

#### RTCP
= Real Time Control Protocol
Se charge de transférer des paquets portant les statistiques sur le transfert et les messages de contrôle entre le serveur et le client.

#### Attaques

##### Tromper la taxation
Cette attaque a pour but de passer les appels gratuits. Le pirate va dissimuler un message SIP dans un message utilisant le RTP/RTCP. Le proxy SIP est donc incapable de détecter le trafic de signalisation alors que le flux de média continuera de transiter. Le CDR (call detail recording) ne sera pas exécuté. Ainsi le pirate peut effectuer des appels téléphoniques gratuit.

##### MITM
= Man In The Middle
Attaque dans lequel un pirate écoute une communication entre 2 interlocuteurs et falsifie les échanges afin de se faire passer pour l’une des parties lors d’un prochain appel.

### IAX
= Inter-Asterisk eXchange
Protocole de voix sur IP développé dans le cadre du projet open source Asterisk.

La version 2 permet les échanges entre client et serveur ainsi qu'entre serveurs. Bien que non standardisé, il est de plus en plus utilisé.
Comparativement aux autres protocoles, la bande passante qu’il utilise pour la transmission des flux de signalisation est beaucoup plus faible. Utilisant uniquement le port UDP 4569, la problématique de NAT est beaucoup plus simple à gérer.

A noter que ses principaux handicaps sont sa diffusion qui reste restreinte ainsi que sa non-interopérabilité avec SIP.

## CODECS
Programmes et protocoles qui vont compresser la voix afin qu’elle soit transmise avec une meilleure qualité.

- G711, coût de bande passante de 64kbits/secondes. 
Sa qualité est bonne, son taux d’utilisation de bande passante est très élevé.
- G729, coût est de 10-30kbits/s, sa qualité est bonne. 
L’utilisation en bande passante est moyenne, voir élevée. C’est le seul à être propriétaire.
- G726, coût en bande passante est de 16, 24, 32, 40kbits/s. 
La qualité est bonne et son utilisation en bande passante est moyen.
- G.723.1, coût en bande passante est ~6,4 kb/s.
La qualité est bonne et son utilisation en bande passante est moyen.
- GSM (Global System for Mobile Communications), coût est de 1,5 à 3.5kbits/seconde.
Qualité est mauvaise, son utilisation en bande passante est très élevée.
- FS-1015/LPC10, coût en bande passante est de 2.4kbits/s.
Sa qualité est très mauvaise, le coût en bande passante est ultra-élevé.
- SPEEX, coût en bande passante est de 2.44kbit/s, 
Qualité bonne/mauvaise, son utilisation bande passante est très élevée à très faible.
- IMBC, coût de bande passante est de 15kbits/s.
Sa qualité est correcte, le coût de la bande passante est moyen.

# IPBX / PABX 
= Internet Private Branch eXchange
= Private Automatic Branch eXchange

Le standard peut être proposé via deux technologies :
- PABX, basé sur RTC 
- IPBX, basé sur IP

## PABX
Standard traditionnel basé sur la téléphonie analogique. 

pas besoin de connexion internet pour faire fonctionner un standard PABX. 
Particulièrement important pour des secteurs comme la santé, les services, les ascensoristes, etc.

Inconvénients : 
- installation, équipements et maintenance sont plus compliqués à gérer que dans le cadre d’un standard IPBX
- installation d’une nouvelle ligne téléphonique est plus fastidieuse avec le PABX
- tarif des communications peut être plus élevé que dans le cas de l’IPBX
- Certaines fonctionnalités ne sont pas accessibles avec le PABX
- Le RTC disparait au profit du tout IP : le PABX ne représente donc pas une solution d’avenir !

Les PABX peuvent accepter de la VOIP grâce à l'ajout d'une carte VoIP.

## IPBX
Basé sur le réseau internet de l’entreprise pour tous les appels téléphoniques.
Ce sont des équipements d’interconnexion des téléphones IP et de gestionnaire central d’appels dans un réseau VOIP.

Avantages :
- Configuration et maintenance sont généralement facilitées,
- Coûts de télécommunications mieux maitrisés,
- Installation de nouvelles lignes est plus rapide qu’avec le PABX,
- Coûts d’exploitation généralement inférieurs à ceux du PABX,
- Beaucoup de services : visioconférences, envoi et partage de fichiers, transfert d’appels ultra simple, routage des appels plus facilement configurable, etc.
- Standards téléphoniques IPBX plus facilement évolutifs que les standards PABX.

# Etude d’une solution de PBX/PABX (ASTERISK)

Logiciel open source destiné à gérer des PABX multi-plateformes.
Système hybride qui peut jouer le rôle d’un autocommutateur privé traditionnel (supportant les lignes analogiques et post-numérique) et d’un PABX supportant des soft phones et des téléphones IP.

Il permet de mettre en place une infrastructure centralisée de VOIP prenant en compte la gestion de tous types de support téléphonique (ligne téléphone analogique, softphones, téléphones IP) et aussi le rôle de passerelle avec les réseaux publics tels que :
- RTC
- RNIS
- GSM

Dans ce cas nous parlons de TRUNK.

Fonctionnalités d'Asterisk :
- Authentification des utilisateurs
- Standard vocal automatique ou IVR (Interactif Voice Response)
- Transfert d’appel
- Service de messagerie vocale
- Gestion des conférences
- Mise en attente
- Facturation détaillée
- Journalisation des appels
- Enregistrement des appels
- Service de messagerie e-mails

