[[Virtual Box]], [[Applications]]
# Virtualisation
## Hyperviseur de type 2
Hyperviseur de type 2 = hosted hypervisor (hyperviseur hébergé)

Hyperviseur de type 2 : adaptés pour de petites infrastructures, pour une seule machine et faire des tests multiplateformes.

S'installe comme une application système et permet de créer des VM indépendantes de l'[[OS]] hôte. Il est donc considéré comme n’importe quelle application et n’a **aucune priorité** sur les ressources de l’hôte.

En revanche, chaque VM est autorisée, par l’hyperviseur, à utiliser une certaine quantité de ressources (définie au départ) et ne peut donc pas dépasser cette limite. L’OS hôte ne pourra donc pas être ralenti par les VM, si elles ont été configurées raisonnablement.

Les utilisations d’un hyperviseur de type 2 sont multiples. Ils sont assez faciles à mettre en place et très efficaces pour répondre aux besoins du type :
-   tester un OS sans formater votre machine physique ;
-   tester ou utiliser régulièrement une application sur un OS en particulier ;
-   simuler une 2e machine et faire des tests de communication simples ;
-   créer un petit réseau de plusieurs VM pour tester des protocoles réseau, des règles de pare-feu, configurer un serveur de supervision ou autre.

## Hyperviseur de type 1
Hyperviseur de type 1 = hyperviseur natif

Hyperviseur de type 1 : adapptés pour des grosses architectures réseaux d'entreprise qui nécessitent des optimisations de coût et de maintenance, tout en améliorant la robustesse face aux pannes.

Installé directement sur le matériel, sans OS intermédiaire. Les ressources de l’hôte sont directement gérées par l’hyperviseur et non plus par l’OS qui **disparaît** ou est **relégué** au statut de VM. La **totalité** des ressources est dédiée aux VM.

Les hyperviseurs de type 1 sont utilisés en entreprise pour plusieurs raisons, comme par exemple :
-   réduire les coûts matériels et de maintenance ;
-   optimiser les ressources physiques ;
-   répartir la charge dynamiquement ;
-   permettre la haute disponibilité des serveurs ;
-   créer des VM de préproduction pour les tester en environnement réel avant de les mettre en production.

## Fichiers ISO
VM Windows 10 directement sur le site de Microsoft : 
[https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)

## Guest Additions
[how-to-install-virtualbox-guest-additions-on-debian-10/](https://linuxize.com/post/how-to-install-virtualbox-guest-additions-on-debian-10/)

```shell
su -
apt update
apt install build-essential dkms linux-headers-$(uname -r)
```
![](https://linuxize.com/post/how-to-install-virtualbox-guest-additions-on-debian-10/insert-guest-additions-cd-image_hu6613c524b7b09bc1b2462026613a9c75_59766_768x0_resize_q75_lanczos.jpg)

``` shell
mkdir -p /mnt/cdrom
mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom`
sh ./VBoxLinuxAdditions.run --nox11
shutdown -r now
```