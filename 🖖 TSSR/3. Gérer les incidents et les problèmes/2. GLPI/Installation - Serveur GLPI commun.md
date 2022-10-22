
# Configuration - Cloud Amazon AWS <a name="IID1"></a>

AWS > EC2 > Wizard

``` shell
#Vérifier les informations de temporalité
date
#Reconfigurer si besoin
dkpg-reconfigure tzdata

```

### Configuration - Apache2 

``` shell
cd /etc/apache2

#Activation module SSL pour HTTPS
a2enmod ssl
systemctl restart apache2

#Voir les modes activés dans Apache2
mods-enable

cd sites-enabled
#Désactiver le site par défault
a2ssite 000-default
rm 000-default
nano site1.conf

nano /var/www/html/index.html
rm -R www

adduser glpi
cd /home/glpi
su glpi
mkdir www
cd www
nano index.html

```

### Création certificat SSL pour connexion HTTPS

Certification gratuite via certbot. Enregistrement de 60 jours, à renouveler régulièrement.

``` shell
cd /root
wget https://del.eff.org/certbot-auto
chmod x certibot-auto
./ certbot-auto
```

### Installation GLPI sur le serveur cloud 

```shell
cd /home/glpi/www
rm index.html
rm /www
cd /home/glpi
wget glpi https://github.com/glpi-project/glpi/releases/download/9.5.5/glpi-9.5.5.tgz
mv glpi www

```
