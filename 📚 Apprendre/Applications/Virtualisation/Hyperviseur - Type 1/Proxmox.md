Environnement complet de gestion centralisée de datacenter, s'appuyant sur l'hyperviseur KVM et le gestionnaire de conteneurs LXC. 
Open source avec support de service payant. 

[Tutoriel installation Proxmox](https://chrtophe.developpez.com/tutoriels/proxmox/)

# Installation
- [ ] Installation à partir d'un [fichier ISO](https://www.proxmox.com/en/downloads/category/iso-images-pve), disponible uniquement pour Debian. 
- [ ] Dans edit virtual settings
> Processor > virtualization engine > cocher virtualize inter...
- [ ] connexion en bridge
- [ ] fixer le disque en espace alloué fixe

## Bug de connexion
Si jamais, lors du lancement de la VM ça ne fonctionne pas : 
Désactiver Hyper V
Puis, commande cmd :
`bcdedit /set hypervisorlaunchtype off`
redémarrer

[Windows 11 - disable Hyper V](https://www.makeuseof.com/windows-11-disable-hyper-v/)
