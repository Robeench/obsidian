[[Protocole]]
# Server Message Block (SMB)
[[Protocole]] client - serveur qui permet d’accéder à des ressources via le réseau., particulièrement des fichiers et des dossiers.
On le retrouve essentiellement sur les réseaux locaux car il a été pensé pour cet usage.
Né en 1985, il été connu sous le nom de CIFS (common internet file system).
Client - Serveur qui permet d’accéder aux ressources (notamment les fichiers).
Installé automatiquement sous [[Windows]]. Et fonctionne sous [[Linux]] via SAMBA.
Le protocole utilise le port 139 ou le port 445. Il n’utilise pas les deux en même temps.

### SMB - [[Port]] 139
Historiquement, il était nécessaire d’établir une connexion sur le port 139. Pour contacter l'hôte, le protocole SMB s'appuyait sur NetBIOS.

### SMB - Port 445
Le protocole s’appuie sur une connexion TCP et le port 445 pour établir une connexion sécurisée entre le client et le serveur. La résolution du nom, pour permettre la connexion, s’appuie sur le [[DNS]].

**Le port 445 est utilisé pour les connexions SMB sur tous les systèmes depuis [[Windows]] 2000.**

## Créer un partage et tester l’accès SMB
Nous avons besoin de :
- une machine avec un partage, qui jouera le rôle de serveur au sein de la connexion SMB ([[Windows]])
- une machine pour accéder aux données, qui jouera le rôle de client dans la connexion SMB ([[Linux]])
- les deux machines font partie d’un même domaine [[Active directory]]