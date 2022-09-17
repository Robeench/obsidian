[[HTML 5]]
# CSS 3
Pour vérifier si mon navigateur peut lire une instruction : [https://www.caniuse.com/](https://www.caniuse.com/)

## Formater du texte
```css
font-size: 1em; /* modifier la taille relative du texte */
font-family: nomdepolice1, nomdepolice2; /* changer la police */

@font-face {
	font-family: 'manouvellepolice';
	src: url('manouvellepolice.eot') format(eot);
} /* force le navigateur à télécharger la police de mon choix */

font-style: italic; oblique; /* texte en oblique */ normal; /* texte en normal par défaut */
font-weight: bold; /* en gras */ normal;
text-decoration: underline; /* souligné */ line-through; /* barré */ overline; /* ligne au dessus */blink; /* clignotant */ none; /* normal par défaut */
text-align: center; left; right; justify; /* alignement du texte */

float: left; right; /* image habillée de texte */
```

Pour trouver des polices cool en libre-service :
[https://www.fontsquirrel.com/](https://www.fontsquirrel.com/)

Pour la taille des éléments, utiliser REM :
[Unité de mesure CSS : REM | Le blog d'Adfab](https://connect.adfab.fr/dev/dev-front/unite-de-mesure-css-rem)

Modifier la capitalisation d'un texte :

```css
text-transform : capitalize; /*première lettre en capitale*/
text-transform : uppercase; /*en majuscules*/
text-transform : lowercase; /*en minuscules*/
text-transform : none;
```

## Liste
```css
ul { 
list-style-type: none; /*enlever le style d'une liste*/
list-style-image: url("images/icone.jpg"); /*mettre une image comme puce*/
} 
```

## Couleur et fond
```css
color: #FFFFFF; /* couleur du texte en hexadécimal */

background-color: #FFFFFF; /*ajouter une couleur de fond*/
background-image: url('imagedefond.jpg'); /* ajouter une image de fond */
background-attachment: fixed; scroll; /* fixer le fond */
background-repeat: no-repeat; repeat-x; /*fond répété sur la première ligne, horizontalement */ repeat-y; /* fond répété sur la première ligne, verticalement */ repeat;
background-position: 30px 50px; 
/* OU */ background: url('imagedefond') fixed no-repeat top right; /* combiner plusieurs propriétés de background */

opacity: 0.5; /* indique le niveau d'opacité, 1 = totalement opaque et 0 = totalement transparent */
background-color: rgba(255, 0, 0, 0.5); /* niveau d'opacité au 4ème paramètre via RGBA, modifie uniquement l'opacité du fond */
```

Pour trouver les différentes couleurs en hexadécimal :
[https://www.webfx.com/web-design/color-picker/](https://www.webfx.com/web-design/color-picker/)

## Bordures et ombres
```css
border: 2px #FFFFFF dashed;
	none; /* pas de bordure */ solid; /* un trait simple */ dotted; /* pointillés */ dashed; /* tirets */ double; groove; /* en relief */ ridge; /* autre effet de relief */ inset; /* effet 3D global enfoncé */ outset; /* effet 3D global surélevé */
border-top; border-bottom; border-left; border-right; /* appliquer un style de bordure à un coin de mon élément */
border-radius: 10px; /* arrondir les angles d'un élément */
box-shadow: 6px 6px 0px black inset /* ombre placée à l'intérieur du bloc */; /* ombre de boite avec 1 = décalage horizontal, 2 = décalage vertical, 3 = adoucissement du dégradé, 4 = couleur */
text-shadow: 2px 2px 4px black;
```

## Centrer un block
[Centrer un bloc horizontalement et verticalement dans une page](https://www.christophe-meneses.fr/article/centrer-un-bloc-horizontalement-et-verticalement-dans-une-page)

## Apparences dynamiques

```css
:hover /* survoler */
:active /* au moment du clic */
:visited /* élément visité */
:focus /* lorsque l'élément est sélectionné */
```

### Smooth scroll
```css
html {
	scroll-behavior: smooth;
}
```

## Sélecteurs CSS
```css
[type='radio'] {
  margin: 20px 0px 20px 0px;
} /*ce sélecteur fonctionne avec les éléments ayant un "type"*/
```

## Variable
```css
--penguin-skin: gray; /*variable*/
background: var(--penguin-skin); /*assigner ma variable à des balises*/
background: var(--penguin-skin, black); /*ajout d'une couleur si jamais le navigateur ne peut pas lire la variable*/
<style>
  :root /*lorsqu'on crée des variables sous root, elles s'héritent sur toute la page*/{
    --penguin-skin: gray;
    --penguin-belly: pink;
    --penguin-beak: orange;
  }

```

## Réglage du remplissage d'un élément

```css
p {
	width: 500px; /*largeur du contenu du block, s'exprime en px ou %*/
	height: 50%; /*hauteur du contenu du block, s'exprime en px ou %*/
}
```

```css
min-width /*largeur minimale*/
min-height /*hauteur minimale*/
max-widht /*largeur maximale*/
max-height /*hauteur maximale*/

p { /*si la page du navigateur est trop petite, le p se force à occuper au moins 400px*/
	width: 50%;
	min-width: 400px;
}
```

**padding** = marge intérieure 

**margin** = marge extérieure

![https://user.oc-static.com/files/5001_6000/5633.jpg](https://user.oc-static.com/files/5001_6000/5633.jpg)

```css
padding: 20px;
padding-top: 10px;
padding-right: 20px;
padding-bottom: 30px;
padding-left: 40px;
/*ou*/ padding: 10px 20px 30px 40px;

margin: 20px;
margin: -20px;
margin-top: 10px;
margin-right: 20px;
margin-bottom: 30px;
margin-left: 40px;
/*ou*/ margin: 10px 20px 30px 40px;
```

### Centrer des block

```css
p
{
    width: 350px; /* On a indiqué une largeur (obligatoire) */
    margin: auto; /* On peut donc demander à ce que le bloc soit centré avec auto */
}
```

### Quand ça dépasse..
Si on veut que le texte ne dépasse pas à l'intérieur d'un petit block, il faut utiliser **overflow**
Si on place un mot très long dans un block et qu'il ne tient pas dans la largeur, **word-wrap** permet de forcer la coupe.

```css
overflow: visible; /*il sort du block*/
					hidden; /*il est coupé*/
					scroll; /*il est coupé mais le navigateur met en place des barres de défilement dans le block*/
					auto; /*le navigateur décide, à utiliser le plus souvent*/

word-wrap: break-word;

```

## Flexbox

```css
<div id="conteneur">
    <div class="element 1">Element </div>
    <div class="element 2">Element </div>
    <div class="element 3">Element </div>
</div>

```

```css
#conteneur
{
    display: flex;
}
```

### Direction
```css
#conteneur {
    display: flex;
    flex-direction: row; /*organisé sur une ligne (par défaut)*/
		column; /*organisé sur une colonne*/
		row-reverse; /*organisé sur une ligne, en ordre inversé*/
		column-reverse; /*organisé sur une colonne, en ordre inversé*/
}
```

### Retour à la ligne

```css
#conteneur {
    display: flex;
    flex-wrap: nowrap; /*pas de retour à la ligne (par défaut)*/
		wrap; /*éléments vont à la ligne lorsqu'il n'y a plus de place*/
		wrap-reverse; /*éléments vont à la ligne en sens inverse, lorsqu'il n'y a plus de place*/
}
```

### Alignement
Les éléments sont organisés horizontalement (par défaut) ou verticalement = c'est l'axe principal.
Il y a aussi un axe secondaire = **cross axis**
-   si mes éléments sont organisés horizontalement, l'axe secondaire est VERTICAL.
-   si mes éléments sont organisés verticalement, l'axe secondaire est HORIZONTAL.
Pour changer l'alignement des éléments, quelque soit l'axe principal, j'utilise **justify-content**.

```css
#conteneur {
    display: flex;
    justify-content: flex-start; /*alignés au début(par défaut)*/
		flex-end; /*alignés à la fin*/
		center; /*alignés au centre*/
		space-between; /*éléments étirés sur tout l'axe avec de l'espace entre eux */
		space-around; /*éléments étirés sur tout l'axe avec espace entre eux + sur les extrémités*/
}
```

Pour changer l'alignement sur l'axe secondaire, on utilise **align-items**.

```css
#conteneur {
	display: flex;
	align-items: stretch; /*éléments étirés sur tout l'axe (par défaut)*/
		flex-start; /*alignés au début*/
		flex-end; /*alignés à la fin*/
		center; /*alignés au centre*/
		baseline; /*alignés sur la ligne de base (semblable à flex-start)*/
```

Il est possible de faire une exception pour un seul des éléments sur l'axe secondaire :

```css
#conteneur {
	display:flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
}

.element:nth-child(2) /*on prend le 2ème block élément*/
{
	background-color: blue;
	align-self: flex-end; /*seul ce bloc sera aligné à la fin*/
}
```

### Répartir plusieurs lignes
Si on a plusieurs lignes dans une Flexbox, on peut choisir comment elles seront réparties avec **align-content**.

```css
#conteneur {
	display: flex;
	align-content: flex-start; /*les éléments placés au début*/
		flex-end; /*éléments placés à la fin*/
		center; /*éléments placés au centre*/
		space-between; /*éléments séparés avec de l'espace entre eux*/
		space-around; /*éléments séparés avec de l'espace entre eux + au début et à la fin*/
		stretch; /*éléments s'étirent pour occuper tout l'espace (par défaut)*/
	}
```

### Ordre des éléments
```css
.element:nth-child(1)
{
    order: 3;
}
.element:nth-child(2)
{
    order: 1;
}
.element:nth-child(3)
{
    order: 2;
}
```
Les éléments sont automatiquement triés du plus petit au plus grand nombre.

### Faire grossir ou maigrir les éléments
```css
.element:nth-child(2)
{
    flex: 1;
}
```
Cela permet à un élément de grossir pour occuper tout l'espace restant. Le nombre que l'on indique dans flex indique dans quelle mesure il peut grossir par rapport aux autres.

```css
.element:nth-child(1) {
	flex: 2;
}
.element:nth-child(2) {
	flex: 1;
}
/*le 1er élément peut grossir 2x plus que le 2ème élément*/
```

La propriété flex est une super-propriété qui combine flex-grow (capacité à grossir), flex-shrink (capacité à maigrir) et flex-basis (taille par défaut).

### Tableau
```css
border-collapse: collapse; /*bordures du tableau html collées entre elles*/
border-collapse: separate; /*bordures du tableau html dissociés*/
td { /*définit la bordure*/
border: 1px solid black;
}

caption-side: top; /* titre placé au dessus du tableau*/
caption-side: bottom; /*titre placé en dessous du tableau*/
```

## Responsive design
### Media queries
Règles applicables dans certaines conditions : résolutions d'écrans, type d'écran, nombre de couleurs, orientation de l'écran...
Utilisable de deux manières :
-   charger une feuille de style .css différente selon la règle
    
    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8" />
            <link rel="stylesheet" href="style.css" /> <!-- Pour tout le monde -->
            <link rel="stylesheet" media="screen and (max-width: 1280px)" href="petite_resolution.css" /> <!-- Pour ceux qui ont une résolution inférieure à 1280px -->
    		</head>
    ```
    
-   écrire la règle directement dans le fichier .css

```css
@media screen and (max-width: 1280px)
{
    /* Rédigez vos propriétés CSS ici */
}
```

### Règles
-   `color` : gestion de la couleur (en bits/pixel) ;
-   `height` : hauteur de la zone d'affichage (fenêtre) ;
-   `width` : largeur de la zone d'affichage (fenêtre) ;
-   `device-height` : hauteur du périphérique ;
-   `device-width` : largeur du périphérique ;
-   `orientation` : orientation du périphérique (portrait ou paysage) ;
-   `media` : type d'écran de sortie. Quelques-unes des valeurs possibles :
    -   `screen` : écran « classique »,
    -   `handheld` : périphérique mobile,
    -   `print` : impression,
    -   `tv` : télévision,
    -   `projection` : projecteur,
    -   `all` : tous les types d'écrans.

On peut rajouter devant chaque règle min- ou max- et elles peuvent être combinées via only, and, et not.

```css
/* Sur les écrans, quand la largeur de la fenêtre fait au maximum 1280px */
@media screen and (max-width: 1280px)

/* Sur tous types d'écran, quand la largeur de la fenêtre est comprise entre 1024px et 1280px */
@media all and (min-width: 1024px) and (max-width: 1280px)

/* Sur les téléviseurs */
@media tv

/* Sur tous types d'écrans orientés verticalement */
@media all and (orientation: portrait)
```

### Navigateurs mobiles

```css
@media all and (max-device-width: 480px)
{
    /* Vos règles CSS pour les mobiles ici */
}

```

Ne pas utiliser handheld, uniquement reconnu par Opera
Les navigateurs mobiles simulent une largeur d'écran (différentes à chaque fois), viewport.

```html
<meta name="viewport" content="width=320" />
<meta name="viewport" content="width=device-width" />
<!--viewport de la même largeur que l'écran-->
```

## Grid
```css
.container {
	display: grid;
	grid-template-column: 50px 50px; /*2 colonnes de 50px*/
	grid-template-rows: 50px 50px; /*2 lignes de 50px*/
	grid-column-gap: 10px; /*crée un gap vide entre les colonnes*/
	grid-row-gap: 10px; /* crée un gap entre les lignes*/
	grid-gap: 10px 20px; /* 1er change les row, 2ème change les column*/
	grid-row: 1 / 3; /*début / fin de l'emplacement de l'item*/
	grid-column: 1 / 3; /*idem*/
	justify-items: start; center; end; /*tous les items*/
	align-items: start; center; end; /*tous les items*/
	grid-template-areas: /*joindre des grid*/
  "header header header"
  "advert content ."
  "footer footer footer";
}
.item1 {
	justify-self: start; center; end; /*horizontal*/
	align-self: start; center; end; /*vertical*/
	grid-area: header; /*je veux l'item1 comme header, je dois d'abord définir le grid-template-areas*/
	grid-area: 1/1/2/4; /*the item will consume the rows between lines 1 and 2, and the columns between lines 1 and 4.*/
}
```