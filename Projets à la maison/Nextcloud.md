# Nextcloud

``` Shell
#Mise à jour dépôts et paquets
apt -y update && apt -y upgrade

#Ajout dépôt php
apt install -y lsb-release apt-transport-https ca-certificates && \
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" |
     tee /etc/apt/sources.list.d/php.list && \
apt update -y

```