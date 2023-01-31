
# Utilisateurs - [[Linux]]
## Création et suppression compte utilisateur
Uniquement utilisable par l'utilisateur root
useradd crée un nouveau compte utilisateur en fonction des options spécifiés dans la ligne de commande et des valeurs par défaut définies dans /etc/default/useradd

```shell
adduser userName1 #crée le compte userName1 avec ses options
passwd userName1 #permet d'entrer et confirmer le mot de passe
userdel userName1 #supprime le compte userName1
```

## Changement utilisateur
```shell
su - userName1 #permet le changement d'utilisateur
```


https://goodmood-photobooth.com/fr/comment-creer-des-utilisateurs-de-linux-commande-useradd/

https://fr.joecomp.com/how-create-users-linux

https://francoandroid.com/comment-changer-un-nom-de-compte-utilisateur-sous-linux/

https://goodmood-photobooth.com/fr/comment-creer-des-utilisateurs-de-linux-commande-useradd/