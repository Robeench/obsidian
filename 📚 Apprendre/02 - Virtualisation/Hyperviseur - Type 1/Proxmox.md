Environnement complet de gestion centralisée de datacenter, s'appuyant sur l'hyperviseur KVM et le gestionnaire de conteneurs LXC. 
Open source avec support de service payant. 

Port par défaut : 8006

# Consignes
- [x] Monter deux serveurs Proxmox (1 processeur, 4 cœurs + 4 Go de RAM + 30 Go ou plus de SSD)
- [x] Mettre en cluster les serveurs promox
- [x] Créer un template de machine virtuelle
- [x] Créer une machine a l'aide de ce template
- [x] Migrer la machine sur proxmox02, puis proxmox03
- [x] Cloner une machine a chaud
- [x] Migrer une machine à chaud
- [ ] Créer un partage externe SMB sur Proxmox 
- [ ] Sauvegarder une machine sur ce partage 
- [ ] Détruisez la machine sauvegardé et la réinstaller via le backup externe
- [ ] Configurez les notifications mail des backup et tester l'envoi de mail
- [ ] Ajout d'un disque supplémentaire de 30Go sur chaque nœud (redémarrer le nœud)  
- [ ] Ajout d'une seconde interface réseau sur chaque nœud
- [ ] Configurer ces secondes interfaces (vmbr1) sur le même réseau 
- [ ] Sur chaque nœud, installer Ceph (via le menu dans l'arborescence)  
- [ ] Configurer les managers puis création des OSD sur chaque nœud  
- [ ] Création des pools de stockage Ceph  
- [ ] Tester les migrations à chaud  
- [ ] Configurer HA  
- [ ] Arrêter proxmox01 et observer la migration à chaud de notre VM sur proxmox02
- [x] Ajout d'un proxmox03 au cluster

# Installation
## Configuration des VM Proxmox

[Tutoriel installation Proxmox sur Developez](https://chrtophe.developpez.com/tutoriels/proxmox/)
[Tutoriel installation Proxmox sur ITConnect](https://www.it-connect.fr/comment-installer-proxmox-ve-7-0-et-creer-sa-premiere-vm/#:~:text=Cliquez%20sur%20%22Proxmox%20VE%207.0,pensez%20%C3%A0%20sauvegarder%20vos%20donn%C3%A9es.)

Installation à partir d'un [fichier ISO](https://www.proxmox.com/en/downloads/category/iso-images-pve), disponible uniquement pour Debian. 
- [ ] Connexion en bridge
- [ ] 1 processeur, 4 cœur (ou 4 processeurs) + 4Go de RAM + 30 Go SSD
- [ ] Vérifier les adresses IP disponibles avec IP Scanner

#### Sous VMWare
Edit virtual machine settings > Processors > Virtualization engine > Virtualize Intel VT-x/EPT or AMD-V/RVI

#### Sous VirtualBox
Configuration > System > Processor > Enable Nested VT-x/AMD-V

### Lancement VM
- Install Proxmox VE
- Accepter License Agreement
- Target HardDisk : disque dur de la VM
proxmox efface les données présentes.
options = pour personnaliser le partitionnement
- Sélection pays + heure + clavier
- Mot de passe et mail administrateur 
id = mail@example.com
mdp = L'informatique ?
- Personnalisation FQDN + réglages réseau
Management interface = carte réseau
hostname = proxmox01.nitou
IP = 192.168.1.107 /24
gateway = 192.168.1.1
DNS server = 80.67.169.12
- Décocher la case "automatically reboot"
- Install
- Enlever l'ISO du storage pour éviter un boot infini en boucle sur celle-ci.

#### Bug de connexion
Si jamais, lors du lancement de la VM ça ne fonctionne pas, sous VMWare Workstation : 
- Désactiver Hyper V
- Puis, commande cmd :
`bcdedit /set hypervisorlaunchtype off`
- Redémarrer
- Ou [Windows 11 - disable Hyper V](https://www.makeuseof.com/windows-11-disable-hyper-v/)

### Console Proxmox
Connexion à la console proxmox : https://192.168.1.107:8006/
Le port de connexion par défaut est 8006, il n'est pas modifiable. On peut contourner ce comportement avec un reverse proxy.

id = root
mdp = L'informatique ?
sélectionner > Linux PAM standard authentication

#### Proxmox01
192.168.1.107 /24
proxmox01.nitou

#### Proxmox02
192.168.1.108 /24
proxmox02.nitou

#### Proxmox03
192.168.1.109 /24
proxmox03.nitou

Ne pas cloner les VM, cela peut poser des problèmes de certificat, bloquant l'accès à la console.

## Cluster
### Au sein du proxmox01
Menu > Cluster > Create Cluster
	Nom du cluster = cluster-nitou
	Réseau du cluster = adresse IP de proxmox01
Menu > Cluster > Join information > Copy Information

### Au sein du proxmox02 et proxmox03
Menu > Cluster > Join Cluster
	Coller les informations précédentes
	Entrer le mdp root

## Machine virtuelle sous Proxmox
### Importer un fichier ISO
Datacenter cluster-nitou > proxmox01 > local (proxmox01) > ISO images > Upload

### Créer une machine virtuelle
Cliquer sur le bouton en haut à droite de l'interface > Create VM

**General**
Node = proxmox01
VM ID = 100
Name = debian100

**OS**
ajout de l'image ISO

#### Installation debian100
Lors de l'installation, si la connexion internet n'est pas repérée et bloque donc l'installation : 
- cliquer sur revenir en arrière jusqu'à arriver au menu de choix
- accéder au shell
- vérifier sur `nano /etc/network/interfaces` que : 
		- définir l'IP en static
		- vérifier que je définis bien l'IP en inet (= IPv4) et pas inet6 (= IPv6)!
- exit et terminer l'installation

#### Template debian100
- supprimer le disque ISO de la VM pour permettre qu'elle ne soit plus rattachée au local-lvm (proxmox01)
- ajouter Add > CloudInit Drive > 
- Transformer debian100 en template



# Fonctionnalité de datacenter

Pour proxmox, un datacenter est le point unique de gestion des ressources : 
- serveur
- espaces de stockage 
- templates de création de VM ou de conteneurs
- ressources réseau (switch)
- pools de ressources (regroupement de ressources sous une même entité)
- VM
- conteneurs