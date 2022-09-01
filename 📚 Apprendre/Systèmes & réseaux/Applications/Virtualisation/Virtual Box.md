
# VirtualBox
VM [[Windows]] 10 directement sur le site de Microsoft : 
[https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)

## Guest Additions

### Sous [[Linux]]
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

### Sous [[Windows]]
https://lecrabeinfo.net/virtualbox-installer-les-additions-invite-guest-additions.html#sur-une-machine-virtuelle-windows
