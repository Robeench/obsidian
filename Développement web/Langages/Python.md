[[Langage]]
# Python
# Affichage du texte
```python
print ("Hello World")
print ("Hello", end = "") # évite le retour à la ligne
print (10)
print (2 + 3)
print (2 - 3)
print (2 * 3)
print (2 / 3)
print (perimetre, aire) #affiche un espace automatiquement avec la virgule 
print (8, 9, 10, sep=",") #je définis ce qui apparaît dans l'espace. Je peux faire pareil pour end.
```

# Répétitions d'instructions
## Appel d'une fonction

```python
from robot import *
from math import *
```

## Boucle for
```python
for loop in range (10):
	print("Bonjour !")
print("Au revoir !"
```

```python
for nombre in range(<debut>, <fin>, <saut>):
```

fait prendre à la variable "nombre" toutes les valeurs entre 0 et 10, avec un saut de 1. On va donc de 0 (inclus) à 10 (non inclus, c'est-à-dire 9 inclus) en faisant "+1" entre chaque valeur :

```python
for nombre in range(0, 10, 1):
   print(nombre, end = " ")
```

Si on veut afficher de manière décroissante avec un début négatif, le saut est négatif :

```python
for nombre in range(20, -21, -5):
   print(nombre)
```

S'il n'est pas précisé, le saut vaut 1.
Et si on à un "début" égal à 0 et un "saut" égal à 1, alors il existe une écriture plus courte. Ainsi :

```python
for nombre in range(0, 10, 1):
#est égal à :
for nombre in range(10):
```

## Déclarer une variable

```python
largeur = 210
longueur = 297
surface = longueur * largeur
```

## Récupérer une entrée
### Lire un nombre entier

```python
nbSachets = int(input())
contenanceSachets = int(input())

print(nbSachets * contenanceSachets)
```

Les résultats ne sont jamais arrondis, les nombres peuvent devenir aussi grands que nécessaire.

### Lire un nombre à virgule

```python
nombre = float(input())
print(nombre * 2)
```

Lorsqu'on travaille avec des nombres à virgules, le résultat affiché n'est pas toujours exact car seulement 17 chiffres avant ou après la virgule sont conservés au maximum.
Les calculs ne sont pas exacts mais approchés, il faut donc privilégier les nombres entiers aux nombres décimaux !
Il ne faut JAMAIS faire de tests d'égalité ou d'inégalité entre des nombres décimaux.
Il faut passer aux nombres décimaux le plus tard possible dans le programme pour éviter les petites erreurs dues à ces approximations.

## Conditionner une action

```jsx
âge = int(input())
if âge < 10:
   print("Accès interdit")

< strictement inférieur
> strictement supérieur
<= inférieur ou égal
>= supérieur ou égal
```

```jsx
nbOeufs = int(input())
if nbOeufs <= 12:
   print("Une boîte suffit")
else:
   print("Plusieurs boîtes nécessaires")
```

## Tester l'égalité et la différence

Il faut faire bien attention à ne pas confondre l'opérateur `==` avec le simple `=`, car les deux ont des rôles très différents :
-   `=` sert à affecter une valeur à une variable ;
-   `==` sert à tester l'égalité de deux valeurs.
Lorsqu'on veut uniquement tester si deux valeurs sont différentes, on utilise l'opérateur `!=`, qui se lit « _différent de_ ».

```jsx
ageMarie = int(input())
ageRobin = int(input())
if ageMarie == âgeRobin:
   print("Marie et Robin ont le même âge")
else:
   print("Marie et Robin n'ont pas le même âge")
```

```jsx
nbPattes = int(input())
if nbPattes != 8:
   print("L'animal n'est pas une araignée")
```

# Les opérateurs booléens

Un opérateur booléen est toujours vrai ou faux.

Le programme suivant :

```python
if prix < 10:
   print("Pas cher")
```

peut aussi s'écrire :

```python
estPasCher = (prix < 10)
if estPasCher:
   print("Pas cher")
```

On a stocké dans la variable estPasCher la valeur de la comparaison du prix, pour la réutiliser plus tard. Elle est soit True soit False.
3 < 10 vaut True et 11 < 10 vaut False.
On peut affecter la valeur True ou False directement à une variable

```python
toujoursVraie = True
if toujoursVraie:
   print("La variable toujoursVraie vaut 'True'")
```

Un programme ne doit jamais contenir de == True ou == False, car il contient déjà cette information.
On peut aussi utiliser les opérateurs and et or :

```python
estSenior = (age >= 60)
estJeune = (age <= 25) and (age >= 12)
reductionPossible = (estSenior or estJeune)
if reductionPossible:
   print("Réduction!")
```

## And
Permet de combiner les deux conditions, qui doivent être vraies en même temps.

```python
age = int(input())
if (age <= 25) and (age >= 12):
  print("carte possible")
else:
  print("carte impossible")
```

## Or
Permet d'avoir au moins l'une des conditions qui soit vraie.

```python
age = int(input())
if (age <= 25) or (age >= 60):
   print("Réduction possible")
else:
   print("Pas de réduction")
```

```python
age = int(input())
if ( (12 <= age) and (age <= 25) ) or (age >= 60):
   print("Réduction possible")
else:
   print("Pas de réduction")
```

## Not
Permet de calculer le contraire d'une condition, car not renvoie le contraire de la valeur qu'on lui donne. On dit qu'on prend la négation de la condition.

```python
age = int(input())
nbKm = int(input())
reductionPossible = ( (12 <= age) and (age <= 25) ) or (age >= 60)
if reductionPossible:
   print("Réduction possible")
else:
   print("Pas de réduction")  
if ( not (reductionPossible) ) and (nbKm >= 5000):
   print("Cadeau")
else:
   print("Pas de cadeau")
```

# Conditions avancées
## Elif
A utiliser lorsqu'il y a de nombreuses conditions à tester

```python
prix = int(input())
if prix >= 300:
   prix = prix - 40  
elif prix >= 200:
   prix = prix - 25
elif prix >= 100:
   prix = prix - 10
print(prix)
```

# Répétitions conditionnées
## While
"Tant que" la condition est vraie, on continue l'exécution de la boucle. Si on utilise une mauvaise condition, il est possible que le programme ne s'arrête jamais.

![http://data.france-ioi.org/Course/common_while/diagram_while_fr_python.png](http://data.france-ioi.org/Course/common_while/diagram_while_fr_python.png)
```python
while motDePasse != secret or âgePersonne <= 3:
   print("Accès refusé : mauvais mot de passe ou personne trop jeune")
   âgePersonne = int(input())
   motDePasse = int(input())
```

# La notation scientifique
Quand un nombre à virgules a bcp de chiffres, il est affiché en notation scientifique.
Soit :

```python
1.524157885840573e+22
```

C'est à dire :

```
1.524157885840573 * (10 * 10 * ... * 10 * 10 * 10)
                     <-  22 fois le nombre 10  ->
```

En mathématique, on va aussi noter cette valeur 1.524157885840573 × 1022, où "1022" se lit "10 exposant 22" et vaut donc "(10 * 10 * ... * 10 * 10 * 10)" avec 22 fois le nombre 10.
Ou bien :

```python
8.1000000162e-17
```

C'est à dire :

```python
8.1000000162  / (10 * 10 * ... * 10 * 10 * 10)
                  <-  17 fois le nombre 10   ->
```

En mathématique, on va aussi noter cette valeur 8.1000000162 × 10-17, où "10-17" se lit "10 exposant moins 17" et vaut donc "1 / (10 * 10 * ... * 10 * 10 * 10)" avec 17 fois le nombre 10.

# Nombres à virgules
## Faire des arrondis
Arrondir un nombre décimal c'est le transformer en entier
floor comme sol = entier inférieur
ceil pour ceiling comme plafond = entier supérieur
round comme arrondi = entier le plus proche

```python
from math import *
# Entier inférieur (partie entière)
arrondiInf = floor(12.3)
print(arrondiInf) #soit 12

# Entier supérieur
arrondiSup = ceil(12.3)
print(arrondiSup) #soit 13

# Entier proche
arrondiPro = round(12.3)
print(arrondiPro) #soit 12
```

Pour les nombres négatifs :

```python
from math import *
# Entier inférieur (partie entière)
arrondiInf = floor(-12.3)
print(arrondiInf) #soit -13

# Entier supérieur
arrondiSup = ceil(-12.3)
print(arrondiSup) #soit -12
```

La fonction round peut prendre un second argument qui définit la précision de l'arrondi (nombre de chiffres après la virgule)

```python
nouveauPrix = round(nouveauPrix, 2)
```

# Opérateurs, division entière et reste

![http://data.france-ioi.org/Course/general_arithmetic_basics/definitions_FR.png](http://data.france-ioi.org/Course/general_arithmetic_basics/definitions_FR.png)

a // b donne le quotient de la division euclidienne de a par b
a % b donne le reste de la division euclidienne de a par b
soit :
quotient = dividende // diviseur
reste = dividende % diviseur

```python
nombre = int(input())
if (nombre % 2) == 0:
   print("Le nombre est pair")
```

## Priorité des opérateurs division entière et reste
Les calculs de quotient et reste de font avant les additions et soustractions, donc ces codes sont équivalents :

```python
print(10 + 20 // 3 + 42 % 5)
print(10 + (20 // 3) + (42 % 5))
```

# Les tableaux
Comme vous le savez, une variable est comme une boîte qui permet de stocker de l'information. Au lieu d'utiliser une boîte pour chaque mois de l'année, une autre solution serait d'utiliser une seule grosse boîte appelée nbJours, et de mettre plusieurs petites boîtes dans la grande. Pour pouvoir identifier ces petites boîtes on leur donne alors un numéro. Ainsi on demandera à lire la valeur de "la petite boîte numéro 5 située dans la boîte 'nbJours'".
Soit :

```python
nbJours = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
print(nbJours[0])
print(nbJours[5])
#affiche 31
#affiche 30
```

Ceci va créer un tableau nbJours contenant 12 valeurs entières. Les positions de ces valeurs (les numéros des petites boîtes) vont de 0 (pour la première) à 11 (pour la dernière). **La numérotation démarre en effet à 0** en Python.

## Modifier les éléments d'un tableau
Par exemple si on souhaite déclarer un tableau de taille 7, modifier les valeurs aux indices 0 et 6, puis lire un entier et le mettre à la position d'indice 3 il faut utiliser le code suivant :

```python
prix = [0] * 7
prix[0] = 124
prix[6] = 421

prix[3] = int(input())
```

## Tableau de taille variable
Code pour créer un tableau de taille 1000 contenant uniquement des zéros :

```python
notes = [0] * 1000
```

## Trier un tableau
```python
# Défini le tableau
poids = [45, 80, 2]
# Tri le tableau en ordre croissant 
poids.sort()
# Affiche le tableau
for indice in range(3):
   print(poids[indice])
```

## Trouver l'index d'une liste
La fonction renvoie l’index de la première occurrence qu’elle trouve à partir de l’index `0` quel que soit le nombre de fois qu’elle apparaît dans la liste.

```python
tableau = [13, 14, 20, 0, 20, 20]
print(tableau.index(20))
# Affiche 2
```

## Affichage simplifié
Pour lire 3 entiers puis les afficher l'un après l'autre, séparés par des tirets :

```python
nombre1 = int(input())
nombre2 = int(input())
nombre3 = int(input())
print("{}-{}-{}".format(nombre1, nombre2, nombre3))
```

Dans le texte `"{}-{}-{}"`, on met un `{}` à chaque endroit où on souhaite placer un entier donc ici, trois entiers séparés par des tirets. Ensuite, on donne comme arguments à la fonction `format()` les trois entiers qu'on veut insérer à la place des `{}`.
Cela marche de la même manière si au lieu d'avoir des entiers vous avez d'autres objets : des nombres à virgules, du texte...

## Tableaux et indices négatifs

```python
hauteurs = [1, 2, 3]
print(hauteurs[0])
print(hauteurs[-1])
print(hauteurs[-2])
print(hauteurs[-3])
# Renvoie : 1 3 2 1
```

## Calculer la taille d'un tableau

```python
hauteur = [10, 48, -5, 99, -20, 4, 32, 16, 0, 100, 42]
tailleHauteur = len(hauteur)
```

# Chaines de caractères
## Lire une ligne de texte

```python
print("Le Corbeau et le Renard")
# Le Corbeau et le Renard

vers = "Maitre Corbeau, sur un arbre perche,"
print(vers)
# Maitre Corbeau, sur un arbre perche,

vers = input()
print(vers)
# Tenait en son bec un fromage.
```

## Comparer deux chaînes de caractères
Permet de comparer deux chaînes selon l'ordre alphabétique ou lexicographique.

```python
ligne1 = "Maitre Renard, par l'odeur alleche,"
ligne2 = "Lui tint a peu pres ce langage :"
print("Selon l'ordre lexicographique, ", end = "")
if ligne1 < ligne2:
   print("la ligne 1 est située avant la ligne 2")
if ligne1 == ligne2:
   print("la ligne 1 est égale à la ligne 2")
if ligne1 > ligne2:
   print("la ligne 1 est située après la ligne 2")
# Selon l'ordre lexicographique, la ligne 1 est située après la ligne 2
```

## Calculer la longueur d'une chaîne de caractères
```python
vers = "Que vous etes joli! Que vous me semblez beau!"
longueur = len(vers)
print(longueur)
# 45
```

## Lire un mot individuellement
La fonction split permet, à partir d'une chaîne de caractères, de la couper en petits morceaux, chaque morceau étant séparé des autres par une espace. La fonction renvoie un tableau de mots, auxquels on peut alors accéder de manière classique.

```python
# Lit toute la ligne
ligne = input()
# Coupe la ligne en un tableau de mots
mots = ligne.split(" ")
# Affiche la ligne puis les deux mots
print(ligne)
print(mots[0])
print(mots[3])

# Cette ligne comporte plusieurs mots
# Cette
# plusieurs
```

Il est aussi possible de lire une ligne de texte et de la couper en mot, en une seule ligne de code :

```python
mots = input().split(" ")
```

Imaginons, par exemple, qu'on ait à lire un entier nb et un mot (de longueur plus petite que 100), tout deux sur la même ligne :
↳ 5 TRUC
et à afficher ensuite nb fois le mot donné :
↳ TRUC TRUC TRUC TRUC TRUC
Avant de voir comment résoudre cet exercice, il faut comprendre qu'en Python on ne peut pas faire autrement que de lire toute la ligne à la fois. Il faut donc être capable d'extraire les mots ou les nombres situés sur une ligne. Par exemple :

```python
elements = input().split(" ")
nb = int(elements[0])
mot = elements[1]
for id in range(nb):
   print(mot, end = ' ')
```

On a utilisé la fonction split() et nous avons converti le premier mot en un entier, car nous savons que ce mot représente un nombre. Si nous ne l'avions pas fait, nous aurions eu l'erreur suivante : TypeError: 'str' object cannot be interpreted as an integer

## Lire plusieurs choses sur la même ligne, écriture simplifiée
### Lire plusieurs mots

On cherche à lire deux mots sur la même ligne, un nom de pays et un nom de ville, puis afficher un petit texte. En utilisant le code input().split(" ") que vous avez déjà vu on obtient le programme suivant :

```python
mots =  input().split(" ")
pays = mots[0]
ville = mots[1]
print("Vous habitez à {} ({})".format(ville, pays))
```

Ce code fonctionne très bien, mais il est possible de l'écrire de manière plus courte et plus agréable à lire. Au lieu de créer un tableau mots contenant deux éléments, on affecte directement la valeur de input().split(" ") aux deux variables pays et ville. :

```python
pays, ville =  input().split(" ")
print("Vous habitez à {} ({})".format(ville, pays))
```

### Lire plusieurs entiers
De manière similaire, si on chercher à lire deux entiers sur la même ligne on peut utiliser input().split(' ') puis qu'on convertisse chaque élément lu en un entier. Par exemple :

```python
mots =  input().split(" ")
longueur = int(mots[0])
largeur = int(mots[1])
print(longueur * largeur)
```

Il est possible de faire plus court, sans devoir convertir les mots un par un en entiers !

```python
longueur, largeur =  map(int, input().split(" "))
print(longueur * largeur)
```

La fonction map() va appeler la fonction int() (son premier argument) sur chacun des élements du tableau donné comme second argument, et va retourner le tableau contenant tous les entiers. On affecte alors les deux éléments de ce tableau aux variables longueur et largeur.

## Caractères
### Accéder aux caractères d'une chaine et les afficher

```python
prenom = "TINTIN"
print(prenom[0])
print(prenom[5])
```

On remarque que pour les chaînes de caractères les indices démarrent à 0. Ainsi, si _longueur_ est la longueur de la chaîne de caractères, alors il est possible d'accéder aux caractères d'indices 0, 1, 2, ..., _longueur_1. C'est donc pareil que pour les tableaux.

### Comparer deux caractères
Vous avez déjà vu comment comparer deux chaînes de caractères selon l'ordre alphabétique, et il est aussi possible de comparer uniquement deux caractères :

```python
nom = "HADDOCK"
if nom[0] < nom[5]:
   print("La lettre d'indice 0 (H) est avant la lettre d'indice 5 (C) dans l'alphabet")
if nom[2] == nom[3]:
   print("La lettre d'indice 2 (D) est égale à la lettre d'indice 3 (D) dans l'alphabet")
if nom[0] > nom[5]:
  print("La lettre d'indice 0 (H) est après la lettre d'indice 5 (C) dans l'alphabet")
```

Il est aussi possible de comparer un caractère d'une chaîne à un caractère directement indiqué dans le code, par exemple :

```python
nom = "DI GORGONZOLA"
if nom[0] == "D":
   print("Le nom commence par la lettre D")
if nom[3] <= "M":
   print("La quatrième lettre (la lettre G) est située avant la lettre M dans l'alphabet")
if nom[2] == " ":
   print("La troisième lettre est un espace !")
```

En Python, un caractère est simplement une chaîne de caractère de longueur 1, on utilise donc des guillemets doubles, comme pour les chaînes de caractères.

### Modifier une chaîne existante
En python, les chaînes de caractères ne sont pas modifiables. Il faut donc passer par d'autres objets comme un tableau de caractères. On peut ensuite convertir ce tableau en chaîne de caractères pour l'afficher plus facilement ensuite.

```python
texte = "Exemple de texte"
caracteres = list(texte)
caracteres[8] = "X"
caracteres[9] = "X"
texte = "".join(caracteres)
print(texte)
# Exemple XX texte
```

# Les fonctions
Une fonction permet d'associer un identifiant à un bloc d'instructions. Lorsque l'on souhaite effectuer plusieurs fois la même chose, il faut chercher à fournir une écriture simplifiée : la fonction.

```python
def ligneÉtoiles():
   for iCol in range(40):
      print("*", end = "")
   print()

ligneÉtoiles()
nombreLu = float(input("Entrez un nombre décimal : "))
print("Le carré de ce nombre est", nombreLu * nombreLu)
ligneÉtoiles()

# ****************************************
# Entrez un nombre décimal : 42.234
# Le carré de ce nombre vaut 1783.710756
# ****************************************

```

## Fonctions à un paramètre
Notre fonction est paramétrable avec un argument _caractere_ (et nous changeons son nom). On place donc le paramètre nommé entre les parenthèses après le nom de la fonction. Au sein de cette fonction, l'identifiant _caractere_ représente une variable, qui a été initialisée à la valeur indiquée lors de l'appel.

```python
def ligneÉtoiles(caractère):
   for iCol in range(40):
      print(caractère, end = "")
   print()
```

## Fonctions à plusieurs paramètres
Il faut avoir défini dans la déclaration de la fonction que celle-ci prend un deuxième paramètre, cette fois un entier, puis modifier les instructions pour qu'elles utilisent la variable correspondante. Comme pour l'appel, on ajoute simplement un paramètre dans la déclaration en le séparant du premier par une virgule. On nommera par exemple ce paramètre _longueur_ :

```python
def ligneCaractères(caractère, longueur):
   for iCol in range(longueur):
      print(caractère, end = "")
   print()
```

Si l'on a défini que la fonction prenait deux paramètres, on ne peut plus l'appeler en n'en fournissant qu'un seul. En Python, il est toutefois possible de rendre certains paramètres facultatifs.

## Modifier une variable à l'intérieur d'une fonction
Dans le cas où l'on modifierait la valeur d'un paramètre, il est important de noter que cette modification n'a d'effet qu'à l'intérieur de la fonction. Si le paramètre a été passé sous la forme d'une variable au moment de l'appel, celle-ci ne sera pas modifiée :

```python
def afficheEtModifie(paramètre):
   print("Début fonction : ", parametre)
   paramètre = 68
   print("Fin fonction : ", parametre)

valeur = 42
print("Début programme :", valeur)
afficheEtModifie(valeur)
print("Fin programme :", valeur)

# Début programme : 42
# Début fonction : 42
# Fin fonction : 68
# Fin programme : 42
```

## La fonction min()
La fonction min() prend deux valeurs et renvoie la petite des deux.

## La valeur de retour
```python
minimum = 100

def min2(entier1, entier2):
   if entier1 < entier2:
      return entier1
   else:
      return entier2

for loop in range(5):
   entier1 = int(input())
   entier2 = int(input())
   if min2(entier1,entier2) < minimum:
      minimum = min2(entier1, entier2)
print(minimum)
```

## Types structurés
### Simples enregistrements
Lorsque l'on a beaucoup de données, il peut s'avérer intéressant de les regrouper sous un seul nom. Imaginons par exemple que l'on ait de nombreux dessins de rectangle à gérer ; on souhaiterait alors pouvoir regrouper ensemble leur nombre de lignes et de colonnes, ainsi que le caractère de remplissage. Il faut alors définir un type : une _structure_ ou _enregistrement_. Nous définissons ci-dessous un type DessinRectangle. Ce code peut être placé n'importe où : dans une fonction, dans une autre structure, ou à l'extérieur de tout bloc.

```python
class DessinRectangle:
   pass
```

Maintenant, on peut définir des variables (des « instances ») de ce type. Nous créons ci-dessous trois rectangles :

```python
rectLong = DessinRectangle()
rectLong.nbLig = 3
rectLong.nbCol = 12
rectLong.motif = '>'

rectHaut = DessinRectangle()
rectHaut.nbLig = 8
rectHaut.nbCol = 2
rectHaut.motif = 'I'

rectGros = DessinRectangle()
rectGros.nbLig = 10
rectGros.nbCol = 15
rectGros.motif = 'O'
```

Dans la suite, on utilise le point `.` pour accéder aux attributs d'une variable de type DessinRectangle. Les attributs fonctionnent comme des variables normales : on peut lire leur valeur ou la modifier.

```python
def dessinerRectangle(rect):
   for iLig in range(rect.nbLig):
      for iCol in range(rect.nbCol):
         print(rect.motif, end = "")
      print()

dessinerRectangle(rectLong)
dessinerRectangle(rectHaut)
dessinerRectangle(rectGros)
```

### Affectations entre enregistrements
Lorsque l'on écrit le nom de la variable qui contient la structure, par exemple pour l'affecter à une autre :

```python
rectX = DessinRectangle()
rectX.nbLig = 5
rectX.nbCol = 4
rectX.motif = 'X'
copie = rectX
```

cela correspond à une référence vers l'instance qui s'y trouve. Ainsi, après l'exécution du code ci-dessus, les deux variables pointent vers la même instance de DessinRectangle, et on peut donc utiliser indifféremment rectX ou copie pour manipuler la valeur.
C'est l'appel `DessinRectangle()` qui crée une nouvelle instance à mettre dans des boîtes.

### Méthodes
Certains langages permettent d'écrire des fonctions à l'intérieur des types structurés ; on appelle ces fonctions des _méthodes_. Une méthode est équivalente à une fonction, sauf qu'au lieu de faire `fonction(instance, ...)`, elle permet d'écrire `instance.fonction(...)`, donc de faire ressortir l'élément dans l'écriture. Dans le corps de la méthode, l'instance est accessible par un mot-clé particulier.

Voici par exemple la structure précédente, avec une méthode pour le dessin :

```python
class DessinRectangle:
   def dessinerRectangle(self):
      for iLig in range(self.nbLig):
         for iCol in range(self.nbCol):
            print(self.motif, end = "")
         print()
```

Avec cette définition, on peut appeler la méthode en écrivant `rectangle.dessinerRectangle()`. On est obligé d'indiquer que `self` est le premier paramètre de la méthode ; car il s'agit de l'instance appelant la fonction.