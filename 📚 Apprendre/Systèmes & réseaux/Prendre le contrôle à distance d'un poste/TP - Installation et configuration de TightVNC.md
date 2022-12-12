# Installation sous Linux

``` bash
apt-get install tightvncserver

# Démarrer le serveur
tightvncserver

# Vérifier que le serveur est bien démarré
ps -edf | grep tightvnc

```

On peut constater que le **port en écoute** est le **5901,** correspondant à la première session graphique. En effet TightVNC server peut être lancé une seconde fois pour une autre session graphique, le port en écoute sera alors le 5902, etc.

[Installer la commande netstat](https://linuxconfig.org/bash-netstat-command-not-found-debian-ubuntu-linux)

``` bash
# Vérifier les ports d'écoute ouverts
netstat -lptun | grep tightvnc
```

## Démarrer automatiquement TightVNC

### Créer le script de gestion du service
```bash
# Créer le script
touch /usr/local/bin/vncserver
nano /usr/local/bin/vncserver

# Ajouter dans ce fichier vide : 
#!/bin/bash
PATH="$PATH:/usr/bin/"
DISPLAY="1"
DEPTH="24"
GEOMETRY="1280x1204"
OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"

case "$1" in
start)
/usr/bin/tightvncserver ${OPTIONS}
;;

stop)
/usr/bin/tightvncserver -kill :${DISPLAY}
;;

restart)
$0 stop
$0 start
;;
esac
exit 0

# Rendre exécutable ce script
chmod +x /usr/local/bin/vncserver
```

# Installation sous Windows 

[TightVNC - Download](https://www.tightvnc.com/download.php)
