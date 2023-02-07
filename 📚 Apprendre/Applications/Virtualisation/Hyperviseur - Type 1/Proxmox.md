Environnement complet de gestion centralisée de datacenter, s'appuyant sur l'hyperviseur KVM et le gestionnaire de conteneurs LXC. 
Open source avec support de service payant. 

Port par défaut : 8006

# Installation

[Tutoriel installation Proxmox](https://chrtophe.developpez.com/tutoriels/proxmox/)

## Configuration
Installation à partir d'un [fichier ISO](https://www.proxmox.com/en/downloads/category/iso-images-pve), disponible uniquement pour Debian. 
Edit virtual machine settings > Processors > Virtualization engine > Virtualize Intel VT-x/EPT or AMD-V/RVI
- [ ] Connexion en bridge
- [ ] 1 processeur, 4 cœur + 4Go de RAM + 30 Go fixe SSD

Puis, connexion à la console proxmox : https://192.168.1.107:8006/
	> sélectionner Linux PAM standard authentication
### Bug de connexion
Si jamais, lors du lancement de la VM ça ne fonctionne pas, sous VMWare Workstation : 
- Désactiver Hyper V
- Puis, commande cmd :
`bcdedit /set hypervisorlaunchtype off`
- Redémarrer
- Ou [Windows 11 - disable Hyper V](https://www.makeuseof.com/windows-11-disable-hyper-v/)

# Fonctionnalité de datacenter

Pour proxmox, un datacenter est le point unique de gestion des ressources : 
- serveur
- espaces de stockage 
- templates de création de VM ou de conteneurs
- ressources réseau (switch)
- pools de ressources (regroupement de ressources sous une même entité)
- VM
- conteneurs