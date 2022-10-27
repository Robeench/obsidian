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

#Installation pré-requis
export DEBIAN_FRONTEND=noninteractive
apt-get install -y apache2 mariadb-server libapache2-mod-php8.1 imagemagick \
php8.1-gd php8.1-mysql php8.1-curl php8.1-mbstring \
php8.1-intl php8.1-imagick php8.1-xml php8.1-zip \
php8.1-apcu redis-server php8.1-redis \
php8.1-ldap smbclient php8.1-bcmath php8.1-gmp \
sudo
```

``` Shell
#Téléchargement NextCloud 24
wget https://download.nextcloud.com/server/releases/latest-24.tar.bz2

#Extraction dans le répertoire /var/www/
tar -xvf latest-24.tar.bz2 -C /var/www/

#Editer le fichier de configuration
nano /etc/apache2/sites-available/nextcloud.conf

#Contenu : 
Alias / "/var/www/nextcloud/"
<Directory /var/www/nextcloud/>
        Require all granted
        AllowOverride All
        Options FollowSymLinks MultiViews
        <IfModule mod_dav.c>
                Dav off
        </IfModule>
        <IfModule mod_headers.c>
                Header always set Strict-Transport-Security "max-age=15552000; includeSubDomains"
        </IfModule>
</Directory>
```

``` Shell
#Activation du site
a2ensite nextcloud.conf

#Activation des modules
a2enmod rewrite
a2enmod headers
a2enmod env
a2enmod dir
a2enmod mime

#SSL
a2enmod ssl
a2ensite default-ssl

#Redémarrage service apache
systemctl restart apache2
```