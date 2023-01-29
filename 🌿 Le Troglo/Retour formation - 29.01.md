# Julien - Graou Coop
## CONFIG À FAIRE
- Intégrer les profils par défaut s'ils sont dispo (compta, appro, caisse1, caisse2 etc)
- Séparer "GDM" et "inscription" dans l'infra ("nos-outils" là), c'est pas la même chose !
- Trouver un moyen d'intégrer un accès au mode "debug" quelque part (lien spécifique dans infra ?)
- Le lien "inventaire" dans l'infra envoie sur "rayons"
- Beaucoup de modules ne sont pas traduits en français (est-ce que c'est fait exprès parce qu'il y a une appli par-dessus ? Exemple du calcul de cde d'achat)
- Identification du coop en caisse (on n'a pas trouvé comment faire ?)
- Le volume des articles est en litres et non en m3 (fiche article)
- La case "disponible dans le point de vente" n'est apparemment pas cochée par défaut sur tous les articles, vérifier
- METABASE ce serait cool ?

## BUGS
- le changement de créneau ne fonctionne pas dans la GDM (une fois celui validé, ça mouline non stop et il ne se passe rien)
- l'inscription des membres crée des instances séparées (on a eu des coops avec le même numéro + une personne qui ne voyait pas les autres membres que ceux qu'elle avait créé.e.s)
- l'inventaire et les rayons (dans les applis) ne marchent juste pas

## DEMANDES DE DEV
- Permettre aux membres la modification de leur mdp à l'intérieur de l'espace membre
- Permettre une recherche d'article avec "et" (c'est "ou" par défaut et on ne peut pas le changer)
- C'était pas demandé mais il y aura probablement des choses à faire en lien avec l'intégration d'odoo/food apps dans l'espace membre créé par nos camarades troglodytes :)

# Benjamin
-   Demande d’injection des comptes génériques
-   Possibilité de créer des groupes de catégorie B et C avec des droits null mais pour être inscrit en base d’Odoo => remonter dans la base du portail collaborateur
-   Bug sur l’onglet membre > membre > membre dans odoo
-   Possibilité de modifier le mdp de son accès espace membre ?
-   Comment récupérer le mot de passe (mot de passe oublié ?)
-   clef hashage des mots de passes ?
-   Est-il possible d’ajouter le dimanche
-   Recherche dans le filtre comment fait on un ‘et’
-   Traduction des colonnes anglais --> français pour le tableau fournisseur
-   Dans inventaire de l’article => Volume en m3 alors que c’est le litre

# Bénédicte
- pas de bouton pour créer un membre dans odoo
- besoin calendrier pdf semaine A B C D
- achat webcam
- droit à l'image + droit RGPD + vidéprotection
- comment récupérer un mdp s'il est perdu et comment le modifier
- recherche d'articles "OU"
- volume, modifier en litre (pas des m3)
- consignes dans les caisses