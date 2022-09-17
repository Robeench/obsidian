[[CSS 3]]
# HTML 5
HTML est un langage qui permet d'écrire et d'organiser le contenu de la page.

## Base
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TITRE DU SITE</title>
    <link rel="stylesheet" href="style.css">
</head>
```

```html
<p></p> <!-- paragraphe -->
<br/> <!-- sauts de ligne -->
<h1></h1> <!-- il existe six niveaux de titres -->
<strong></strong> <em></em> <mark></mark> <!-- permettent de mettre en valeur certains mots -->
<ul></ul> <!-- liste à puces, non ordonnée--> <ol></ol> <!-- liste à puces ordonnée -->
<li></li> <!-- balise permettant d'insérer les éléments de la liste à puces -->

<div></div> <!--permet d'imbriquer plusieurs éléments en un seul-->
<button type="button">Click Me!</button>
```

## Structurer sa page
### Balises block et inline
[Mémento des balises HTML](https://openclassrooms.com/fr/courses/1603881-apprenez-a-creer-votre-site-web-avec-html5-et-css3/1608357-memento-des-balises-html)

```html
<header>
    <!-- En-tête de la page : logo, bannière, slogan du site -->
</header>

<footer>
    <!-- Pied de page : liens de contact, nom de l'auteur, mentions légales -->
</footer>

<nav> <!-- Menu du site -->
    <ul>
        <li><a href="index.html">Accueil</a></li>
        <li><a href="forum.html">Forum</a></li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</nav>

<section> <!-- regroupe des contenus en fonction de leur thématique -->
    <h1>Ma section de page</h1>
    <p>Bla bla bla bla</p>
</section>

<aside>
    <!-- Placez ici des informations complémentaires -->
</aside>

<article> <!-- portion autonome de la page, qui pourrait être reprise sur un autre site -->
    <h1>Mon article</h1>
    <p>Bla bla bla bla</p>
</article>
```

![https://user.oc-static.com/files/343001_344000/343677.png](https://user.oc-static.com/files/343001_344000/343677.png)

### Balises universelles

```html
<span></span> <!-- balise inline -->
<div></div> <!-- balise block -->
```

Il faut TOUJOURS utiliser la balise la plus adaptée avant d'utiliser une balise universelle. Cela permet d'améliorer la position de ses pages au sein d'un résultat de recherche.

## Liens
```html
<a href="<https://openclassrooms.com>"> <!-- pour insérer un lien, la balise a avec l'attribut href qui indique l'adresse de la page cible -->
<a href="page2.html"> <!-- lien vers une autre page de son site en écrivant le nom du fichier -->
<h1 id="ancre"> <!-- l'attribut id donne un nom unique à une balise, il crée une ancre -->
<a href="#ancre"> <!-- lien vers une ancre -->
```

## Images
Il existe plusieurs formats d'images adaptés au web :
- JPEG : pour les photos
- PNG : pour toutes les autres illustrations
- GIF : similaire au PNG, plus limité en nombre de couleurs mais peut être animé

```html
<img src="" alt=""/> <!-- insérer une image + src = nom de l'image + alt = courte description de l'image -->
<figure></figure> <!-- la figure est pour les éléments qui viennent enrichir/illustrer le texte, l'élément n'est pas seulement décoratif. Elle peut être hors d'un paragraphe -->
<figcaption></figcaption> <!-- insérer une légende au sein d'une figure -->
```

## Formulaire
```html
<form action="<https://freecatphotoapp.com/submit-cat-photo>"> <!--formulaire DATA via HTML-->
	<input type="text" required <!--oblige à remplir le formulaire--> placeholder="cat photo url"<!--donnée pour l'utilisateur-->> 
	<button type="submit">Submit</button> 
</form> 

<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor">Indoor </label>
<!--réponse à clic, pour une réponse-->

<label for="loving"><input id="loving" value="loving" type="checkbox" name="personality">Loving</label>
<label for="caring"><input id="caring" value="caring" type="checkbox" name="personality">Caring</label>
<!--réponse à clic, pour plusieurs réponses-->

<input type="radio" name="test-name" checked> <!--coche d'office le bouton-->
```

## Tableau
```html
<table> <!--tableau-->
	<caption>Passagers du vol 377</caption> <!--titre du tableau-->

	<tr> <!--ligne-->
		<th>Nom</th> <!--En-tête du tableau-->
		<th>Age</th>
		<th>Pays</th>
	</tr>
	<tr> 
		<td>Carmen</td> <!--cellules-->
		<td>33 ans</td>
		<td>Espagne</td>
	</tr>
	<tr>
    <td>Michelle</td>
    <td>26 ans</td>
    <td>États-Unis</td>
  </tr>
</table>
```

![https://user.oc-static.com/files/5001_6000/5706.png](https://user.oc-static.com/files/5001_6000/5706.png)

### Diviser un tableau
```html
<thead></thead> <!--en-tête-->
<tfoot></tfoot> <!--pied du tableau-->
<tbody></tbody> <!--corps-->
```

Il faut écrire les balises dans l'ordre ci-dessus.

### Fusionner des cellules
```html
<td colspan="2"> <!--fusion de colonnes : horizontalement-->
<td rowspan="3"> <!--fusion de lignes : verticalement-->

```

Le chiffre correspond au nombre de cellules fusionnées.
Exemple fusion horizontale :

```html
<table>
   <tr>
       <th>Titre du film</th>
       <th>Pour enfants ?</th>
       <th>Pour adolescents ?</th>
   </tr>
   <tr>
       <td>Massacre à la tronçonneuse</td>
       <td >Non, trop violent</td>
       <td>Oui</td>
   </tr>
   <tr>
       <td>Les bisounours font du ski</td>
       <td>Oui, adapté</td>
       <td>Pas assez violent...</td>
   </tr>
   <tr>
       <td>Lucky Luke, seul contre tous</td>
       <td colspan="2">Pour toute la famille !</td>
   </tr>
</table>
```

![https://s3-eu-west-1.amazonaws.com/sdz-upload/prod/upload/Capture d’écran 2016-05-26 à 16.25.38.png](https://s3-eu-west-1.amazonaws.com/sdz-upload/prod/upload/Capture%20d%E2%80%99e%CC%81cran%202016-05-26%20a%CC%80%2016.25.38.png)

Exemple verticale :
```html
<table>
   <tr>
       <th>Titre du film</th>
       <td>Massacre à la tronçonneuse</td>
       <td>Les bisounours font du ski</td>
       <td>Lucky Luke, seul contre tous</td>
   </tr>
   <tr>
       <th>Pour enfants ?</th>
       <td>Non, trop violent</td>
       <td>Oui, adapté</td>
       <td rowspan="2">Pour toute la famille !</td>
   </tr>
   <tr>
       <th>Pour adolescents ?</th>
       <td>Oui</td>
       <td>Pas assez violent...</td>
   </tr>
</table>
```

![https://user.oc-static.com/files/344001_345000/344374.png](https://user.oc-static.com/files/344001_345000/344374.png)

## Formulaires
La balise form comprend deux attributs :
**method** = indique par quel moyen les données sont envoyées
**get** = limitée à 255 caractères, envoyés dans l'adresse de la page.
**post** = permet d'envoyer un grand nombre d'informations, les données ne transitent pas par la barre d'adresse.
**action** = adresse de la page ou du programme qui va traiter l'information.

```html
<form method="post" action="traitement.php">
	<p>
	</p>
</form>
```

### Zone de saisie simple

Il existe deux zones de textes différentes :
- monoligne : on ne peut y écrire qu'une seule ligne, sert à saisir des textes courts types pseudo, via **input**
- multiligne : permet d'écrire plusieurs lignes, via **textarea**
La balise **input** comprend plusieurs attributs **obligatoires** et **autres** :
**type** = on trouve ici les différents type d'input :
[HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp)

**name** = définit le nom de la zone texte
**id** = identifie l'élément HTML pour pouvoir y accéder et le manipuler, unique pour un élément
**size** = agrandir le champ (en nombre de caractères)
**maxlenght** = limiter le nombre de caractères saisis
**value** = préremplir le champ avec une valeur par défaut
**placeholder** = donner une indication sur le contenu du champ, elle disparait dès que le visiteur clique à l'intérieur du champ

```html
<form method="post" action="traitement.php">
	<p>
		<label for="pseudo">Votre pseudo</label>
		<input type="text" name="pseudo" id="pseudo"/>
	</p>
</form>
```

La balise **label** comprend un attribut :
**name** = se réfère à la variable du formulaire que l'élément concerne

```html
<form method="post" action="traitement.php">
   <p>
       <label for="ameliorer">Comment pensez-vous que je pourrais améliorer mon site ?</label><br />
       <textarea name="ameliorer" id="ameliorer"></textarea>
   </p>
</form>
```

On peut ajouter des attributs à **textearea** :
**rows** = nombre de ligne de texte affichées simultanément
**cols** = nombre de colonnes affichées simultanément
On peut préremplir **textarea** avec une valeur par défaut, au lieu d'utiliser l'attribut **value**.

### Éléments d'options
#### **Cases à cocher**

```html
<form method="post" action="traitement.php">
   <p>
       Cochez les aliments que vous aimez manger :<br />
       <input type="checkbox" name="frites" id="frites" /> <label for="frites">Frites</label><br />
       <input type="checkbox" name="steak" id="steak" /> <label for="steak">Steak haché</label><br />
       <input type="checkbox" name="epinards" id="epinards" /> <label for="epinards">Epinards</label><br />
       <input type="checkbox" name="huitres" id="huitres" /> <label for="huitres">Huitres</label>
   </p>
</form>
```

Il faut donner un nom différent à chaque case à cocher, pour identifier ensuite celles qui ont été cochées par le visiteur.
Pour qu'une case soit cachée par défaut, l'attribut **checked** :

```html
<input type="checkbox" name="choix" checked />
```

#### Regrouper les champs

```html
<form method="post" action="traitement.php">
 
   <fieldset>
       <legend>Vos coordonnées</legend> <!-- Titre du fieldset --> 

       <label for="nom">Quel est votre nom ?</label>
       <input type="text" name="nom" id="nom" />

       <label for="prenom">Quel est votre prénom ?</label>
       <input type="text" name="prenom" id="prenom" />
 
       <label for="email">Quel est votre e-mail ?</label>
       <input type="email" name="email" id="email" />

   </fieldset>
```

#### Attributs divers
On peut placer automatiquement le curseur dans un champ du formulaire avec l'attribut autofocus.
Champ obligatoire = required
#### Bouton d'envoi

```html
<input type="submit" value="Envoyer" action="#"/>
<!--conduit à la page de l'attribut action-->
<input type="reset"> <!--remise à zéro du formulaire-->
<input type="image" src="#"> <!--submit sous forme d'image-->
<input type="button"> <!--bouton générique qui n'a par défaut aucun effet-->

```

## Audio et vidéo
### Formats audio
MP3 : le plus vieux, et le plus compatible
AAC : utilisé majoritairement par Apple sur Itunes
Ogg : format libre
WAV : format non compressé

### Formats vidéo
Format conteneur : boite qui permet de contenir les éléments ci-dessus
codec audio : format du son de la vidéo
codec vidéo : format qui compresse les images
H.264 : l'un des plus puissants et utilisés mais n'est pas 100% gratuit
Ogg Theora : codec gratuit et libre de droits mais moins puissant. Bien reconnu sous [[Linux]], demande des programmes à installer sous [[Windows]]
WebM : codec gratuit et libre de droits proposé par Google, concurrent le plus sérieux de H.264
Pour convertir une vidéo dans ses différents formats :
[Miro Video Converter](http://www.mirovideoconverter.com/)

### Insertion d'un élément audio
-   `controls` : pour ajouter les boutons « Lecture », « Pause » et la barre de défilement.
-   `width` : pour modifier la largeur de l'outil de lecture audio ;
-   `loop` : la musique sera jouée en boucle ;
-   `autoplay` : la musique sera jouée dès le chargement de la page (évitez d'en abuser, c'est en général irritant d'arriver sur un site qui joue de la musique tout seul !) ;
-   `preload` : indique si la musique peut être préchargée dès le chargement de la page ou non. Cet attribut peut prendre les valeurs :
    -   `auto` (par défaut) : le navigateur décide s'il doit précharger toute la musique, uniquement les métadonnées ou rien du tout,
    -   `metadata` : charge uniquement les métadonnées (durée, etc.),
    -   `none` : pas de préchargement. Utile si vous ne voulez pas gaspiller de bande passante sur votre site.
    
    ```html
    <audio controls>
        <source src="hype_home.mp3">
        <source src="hype_home.ogg">
    		Veuillez mettre à jour votre navigateur.
    </audio>
    ```
    
### Insertion d'un vidéo
 -   `poster` : image à afficher à la place de la vidéo tant que celle-ci n'est pas lancée. Par défaut, le navigateur prend la première image de la vidéo, il est mieux d'en créer une via une capture d'écran.
    -   `controls` : pour ajouter les boutons « Lecture », « Pause » et la barre de défilement.    
    -   `width` : pour modifier la largeur de la vidéo.    
    -   `height` : pour modifier la hauteur de la vidéo.
    -   `loop` : la vidéo sera jouée en boucle.
    -   `autoplay` : la vidéo sera jouée dès le chargement de la page.
    -  `preload` : indique si la vidéo peut être préchargée dès le chargement de la page ou non. Cet attribut peut prendre les valeurs :
        -   `auto` (par défaut) : le navigateur décide s'il doit précharger toute la vidéo, uniquement les métadonnées ou rien du tout ;
        -   `metadata` : charge uniquement les métadonnées (durée, dimensions, etc.) ;
        -   `none` : pas de préchargement. Utile si vous souhaitez éviter le gaspillage de bande passante sur votre site.
        
        ```html
        <video controls poster="sintel.jpg" width="600">
            <source src="sintel.mp4">
            <source src="sintel.webm">
            <source src="sintel.ogv">
        		Veuillez mettre à jour votre naviagteur.
        </video>
        ```