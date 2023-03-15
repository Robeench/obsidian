# Guest Additions

## Sous [[Linux]]
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

## Sous [[Windows]]
https://lecrabeinfo.net/virtualbox-installer-les-additions-invite-guest-additions.html#sur-une-machine-virtuelle-windows

# Clonage 
Lors du clonage, l'identifiant unique (SID) de Windows reste le même.
Pour éviter tout conflit, il faut regénérer un nouvel identifiant unique : 
``` shell
cd C:\Windows\System32\Sysprep
sysprep
# Ouverture de l'application "Outil de préparation système"
```

🗂 Entrer en mode OOBE
	Généraliser
		Arrêter le système ou Redémarrer
			Ok

Suite au redémarrage, la configuration initiale de Windows va se lancer comme au premier démarrage, cela permettra la réinitialisation du SID. 
Pour autant, les données ne seront pas supprimées et les applications seront conservées.

## Ressources
[IT-Connect - Comment cloner une machine virtuelle](https://www.it-connect.fr/comment-cloner-une-vm-virtualbox/#III_Mefiance_lorsquune_machine_est_clonee)