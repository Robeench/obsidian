= Virtual Network Computing

Il s'appuie sur le protocole RFB. Grâce à lui, il peut s'abstraire complètement de l'OS. 

# Prise de contrôle
- serveur VNC, installé sur la machine cible
- client VNC, installé sur la machine dont je souhaite prendre le contrôle
- protocole d'échange, le RFB

## Serveur VNC
logiciel s'installant sur la machine que je souhaite controler à distance. 
Il ouvre un port permettant au client de s'y connecter. 
Port par défaut : 5900

## Client VNC
lors de la connexion, j'indique au client l'adresse IP ou le nom de domaine résolu du serveur + le port d'écoute. 

## Communication
![[15384920330272_01.png]]

# Solutions VNC

- Real VNC
- Apple Remote Desktop
- KRDC sous KDE
- Ultra VNC
- Tight VNC