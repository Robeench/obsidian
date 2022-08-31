[[Langage]]
# Javascript
## Déclarez une variable
```jsx
let numberOfCats = 2;
let numberOfDogs = 4;
```

## Modifiez la valeur d'une variable
Pour modifier une variable, on peut simplement la réaffecter. Il n'est pas nécessaire d'utiliser let car la variable a déjà été déclarée :

```jsx
let numberOfCats = 3;
numberOfCats = 4;
```

### Opérateurs arithmétiques
#### Addition et soustraction
```jsx
let totalCDs = 67;
let totalVinyls = 34;
let totalMusic = totalCDs + totalVinyls;
```

```jsx
let cookiesInJar = 10;
let cookiesRemoved = 2;
let cookiesLeftInJar = cookiesInJar - cookiesRemoved;
```

Pour ajouter ou soustraite un nombre d'une variable on peut utiliser les opérateurs += ou -+

```jsx
let cookiesInJar = 10;
/* manger deux cookies */
cookiesInJar -= 2;  //il reste 8 cookies
/* cuisson d'un nouveau lot de cookies */
cookiesInJar += 12; // il y a maintenant 20 cookies dans la boîte
```

On peut aussi utiliser ++ ou — pour ajouter ou soustraire 1

```jsx
let numberOfLikes = 10;
numberOfLikes++;  // cela fait 11
numberOfLikes--; // et on revient à 10...qui n'a pas aimé mon article ?
```

#### Multiplication et division

```jsx
let costPerProduct = 20;
let numberOfProducts = 5;
let totalCost = costPerProduct * numberOfProducts;
let averageCostPerProduct = totalCost / numberOfProducts;
```

Les opérateurs *= et /= peuvent multiplier ou diviser un nombre

```jsx
let numberOfCats = 2;
numberOfCats *= 6;  // numberOfCats vaut maintenant 2*6 = 12;
numberOfCats /= 3;  // numberOfCats vaut maintenant 12/3 = 4;
```

### Mutabilité des variables
Une variable est mutable, elle peut changer au cours du temps

## Découvrir les constantes
Certaines données ne sont pas modifiés pendant l'exécution d'un programme. Pour s'assurer de ne pas réaffecter par erreur des nouvelles valeurs, on utilise une constante.
Ce sont des variables non mutables.

```jsx
const nombrePostParPage = 20;
nombrePostParPage = 30; // Retournera une erreur dans la console car on ne peut plus changer sa valeur
```

# Enregistrez vos données avec des types de données
## Qu'est ce qu'un type ?
Le type d'une variable ou d'une constante est le genre de données qu'elle enregistre. Il y a 3 types primitifs (= briques de base de chaque structure de données) principaux :
-   number (nombre)
-   string (chaine de caractères)
-   boolean (valeur logique)

Il n'est pas nécessaire de déclarer le type d'une variable en javascript.

Javascript est un langage à type dynamique et à typage faible. Cela signifie qu'une variable peut être initialisé en nombre puis réaffecté comme chaine ou autre. Cela offre une grande souplesse mais peut aussi conduire à des comportements inattendu.

Il y a 3 autres types de données primitives :
-   null
-   undefined
-   symbol
Pour plus d'infos : [Structures de données - JavaScript | MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Data_structures)

## Le type number
Les variables de type number peuvent être positives ou négatives. Elles peuvent aussi être des nombres entiers (= outier ou integers) ou décimaux (= virgule flottante ou floating-point).

### Attention à l'arithmétique en virgule flottante
Elle peut déclencher des erreurs très gênantes :

```jsx
let integerCalculation = 1 + 2;  // donne 3
let weirdCalculation = 0.1 + 0.2;  // on attend 0.3, réponse réelle 0.30000000000000004
```

Utilisez au maximum des calculs entiers (pour des prix, plutôt en centimes qu'en euros)

## Le type boolean
Elles ne peuvent avoir que deux valeurs, true ou false.

```jsx
let userIsSignedIn = true;
let userIsAdmin = false;
```

## Le type string
Elles permettent d'enregistrer du texte dans des variables javascript.

```jsx
let firstName = "Will";
let lastName = 'Alexander';
```

Elles peuvent être concaténées (ajoutées à la suite l'une de l'autre) par +

```jsx
let wholeName = firstName + " " + lastName;
```

Il est possible d'utiliser la string interpolation qui permet d'injecter une variable dans le code avec l'expression ${maVariable}

```jsx
const myName = "Alexander";
const salutation = "Bienvenue sur mon site ${myName}!";
console.log(salutation);   //retournera “Bienvenue sur mon site Alexander!”
```

# Définissez des objets et leurs attributs avec des classes
Dans la vie réelle, on remarque des points communs entre différents objets qui crée une représentation mentale d'une catégorie d'objets. Par exemple les livres ont tous une couvertue, un certain nombre de pages, un titre, un ou plusieurs auteurs... L'objet est un type javascript complexe.
En programmation, la liste mentale est une classe.

## Découvrez les objets
Les objets javascript sont écrits en JSON (Javascript Object Notation). Ce sont des séries de paires clés-valeurs. Les objets peuvent être enregistrés dans une variable :

```jsx
let myBook = {
title: "The Story of Tau",
author: "Will Alexander",
numberOfPages: 250,
isAvailable: true
};
```

Chaque clé est une chaine et les valeurs associées peuvent avoir tout type de données.
Les objets permettent de regrouper une chose unique à un même emplacement.

### Accédez aux données d'un objet
Une fois qu'un objet est enregistré dans une variable, on peut accéder à ses données :

```jsx
let myBook = {
title: "L'Histoire de Tao",
author: "Will Alexander",
numberOfPages: 250,
isAvailable: true
};
let bookTitle = myBook.title;  // "L'Histoire de Tao"
let bookPages = myBook.numberOfPages  // 250
```

### Bracket notation
Pour accéder à un sous-élément, on peut utiliser les brackets avec la valeur du sous-élément

```jsx
let myBook = {
   title: "L'Histoire de Tao",
   author: "Will Alexander",
   numberOfPages: 250,
   isAvailable: true
};
let bookTitle = myBook["title"];  // "L'Histoire de Tao"
let bookPages = myBook["numberOfPages"];  // 250
```

On va pouvoir mettre entre bracket une variable qui contient en string le nom de la propriété que l'on souhaite atteindre :

```jsx
let myBook = {
   title: "L'Histoire de Tao",
   author: "Will Alexander",
   numberOfPages: 250,
   isAvailable: true
};
let propertyToAccess = "title"
let bookTitle = myBook[propertyToAccess];  // "L'Histoire de Tao"
```

## Manipulez des classes
La bracket notation convient pour des objets simples et uniques. Pour bcp d'objets du même type, j'utilise les classes.
Une classe est un modèle pour un objet dans le code.

```jsx
class Book {
constructor(title, author, pages) {
this.title = title;
this.author = author;
this.pages = pages;
}
```

Une fois la classe créée, on peut créer des instances via le mot clé new

```jsx
let myBook = new Book("L'Histoire de Tao", "Will Alexander", 250);
/// Cette ligne crée l'objet suivant :
{
title: "L'Histoire de Tao",
author: "Will Alexander",
pages: 250
}
```

# Regroupez ses données avec les tableaux et objets
## Utiliser un array pour enregistrer une liste ordonnée d'éléments
Pour créer un array (=tableau) vide :

```jsx
let guests = [];
```

Ou créer un array rempli avec les éléments voulus :

```jsx
let guests = ["Sarah Kate", "Audrey Simon", "Will Alexander"];
```

On peut ensuite accéder aux éléments de l'array par leur indice (il commence à 0!) :

```jsx
let firstGuest = guests[0]; // "Sarah Kate"
let thirdGuest = guests[2]; // "Will Alexander"
let undefinedGuest = guests[12] // undefined
```

## Utilisez des valeurs plutôt que des références
Les types primitifs sont passés par valeur, cela signifie que c'est toujours une valeur qui est prise en compte et qu'aucun lien n'est maintenu entre les deux variables, par exemple :

```jsx
let numberOfGuests = 20;
let totalNumberOfGuests = numberOfGuests; // 20
```

Par contre, pour les objets et tableaux, ils sont passés par référence. On passe des références aux objets plutôt qu'une valeur des données qu'ils contiennent.

```jsx
let artistProfile = {
name: "Tao Perkington",
age: 27,
available: true
};
let allProfiles = [artistProfile]; // nouveau tableau contenant l'objet ci-dessus
artistProfile.available = false; // modification de l'objet
console.log(allProfiles) // affiche { nom: "Tao Perkington", âge: 27, disponible: false }
```

[Explaining Value vs. Reference in Javascript](https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0)

## Travaillez sur les tableaux
### Le comptage d'éléments
length indique le nombre d'éléments contenus dans un tableau.

```jsx
let guests = ["Will Alexander", "Sarah Kate", "Audrey Simon"];
let howManyGuests = guests.length; // 3
```

### L'ajout et la suppression d'éléments
push pour ajouter un élément à fin d'un tableau :

```jsx
guests.push("Tao Perkington"); // ajoute "Tao Perkington" à la fin de notre tableau guests
```

unshift pour ajouter un élément au début du tableau :

```jsx
guests.unshift("Tao Perkington"); // "Tao Perkington" est ajouté au début du tableau guests
```

pop pour supprimer le dernier élément d'un tableau :

```jsx
guests.pop(); // supprimer le dernier élément du tableau
```

# Choisir la condition appropriée pour contrôler le déroulement de mon programme
Lorsque le programme est de plus en plus évolué, la création de lignes de code qui s'exécutent l'un après l'autre dans un ordre défini ne sera plus possible. Il est alors nécessaire de mettre en place un déroulement de programme. Il va décrire l'ordre dans lequel s'exécutent mes lignes de code. Certaines lignes seront lues une seule fois, certaines plusieurs fois et d'autres complètement ignorées, selon la situation.

## Les instructions if/else
C'est une instruction conditionnelle car elle vérifie que certaines conditions sont réunies et réagit en conséquence
IF (SI) l'utilisateur est connecté, ouvrir sa page d'accueil
ELSE (SINON) revenir à la page de connexion

### Utiliser des valeurs boolean
Si on utilise une valeur boolean simple :

```jsx
if (myBoolean) {
// réaction à la valeur vraie de myBoolean
} else {
// réaction à la valeur faux de myBoolean
}
```

Par exemple pour vérifier qu'un utilisateur est connecté :

```jsx
let UserLoggedIn = true;
if (UserLoggedIn) {
   console.log("Utilisateur connecté!");
} else {
   console.log("Alerte, intrus!");
}
```

### Utilisez des expressions
On peut aussi utiliser des expressions de comparaison qui comparent des valeurs entre elles.
-   < : inférieur à
-   <= : inférieur ou égal à
-   == : égal à
-   > = : supérieur ou égal à
-   > : supérieur à
-   != : différent de

Par exemple

```jsx
const numberOfSeats = 30;
const numberOfGuests = 25;
if (numberOfGuests < numberOfSeats) {
// autoriser plus d'invités
} else {
// ne pas autoriser de nouveaux invités
}
```

On peut aussi chainer les instructions if/else pour réagir à des conditions potentielles multiples

```jsx
if (numberOfGuests == numberOfSeats) {
// tous les sièges sont occupés
} else if (numberOfGuests < numberOfSeats) {
// autoriser plus d'invités
} else {
// ne pas autoriser de nouveaux invités
}
```

Ce chainage va permettre de prévoir différents résultats en fonction de différentes situations

## L'égalité == ou ====
== : égalité simple qui vérifie la valeur mais pas le type donc 5 == "5" renvoie true
=== : égalité stricte qui vérifie à la fois la valeur et le type donc 5 === "5" renvoie false
De même, il y a deux opérateurs d'inégalité != et !== avec la même distinction.

### Les conditions multiples
Parfois on veut vérifier plusieurs conditions pour un même résultat, par exemple dans la même instruction if. Pour cela il existe des opérateurs logiques.
-   && : ET logique pour vérifier si deux conditions sont toutes les deux vraies
-   || : OU logique pour vérifier si au moins une condition est vraie
-   ! : NON logique pour vérifier si une condition n'est pas vraie

```jsx
let userLoggedIn = true;
let hasUserPremiumAccount = true;
let userHasMegaPremiumAccount = false;

userLoggedIn && userHasPremiumAccount; // true
userLoggedIn && userHasMegaPremiumAccount; // false

userLoggedIn || userHasPremiumAccount; // true
userLoggedIn || userHasMegaPremiumAccount; // true

!userLoggedIn; // false
!userHasMegaPremiumAccount; // true
```

## Le scope des variables
Les variables créées par let ou const ne peuvent être lues ou utilisées qu'à l'intérieur du bloc de code (soit entre {}) dans lequel elles sont déclarées.

Vous rencontrerez certainement le mot clé var pour la création de variables au cours de votre carrière de développeur. Les variables déclarées ainsi n'ont pas un scope de bloc mais un scope de fonction ; donc elles n'ont pas tout à fait le même comportement que celles que je décris dans ce cours. Pour plus d'informations, je vous conseille cet article (en anglais) : [https://www.geeksforgeeks.org/difference-between-var-and-let-in-javascript/](https://www.geeksforgeeks.org/difference-between-var-and-let-in-javascript/)

Dans ce code nous avons deux blocs de code

```jsx
let userLoggedIn = true;

if (userLoggedIn) {
   let welcomeMessage = 'Welcome back!';
} else {
   let welcomeMessage = 'Welcome new user!';
}

console.log(welcomeMessage); // renvoie une erreur
```

Ces variables ne sont disponibles qu'à l'intérieur du bloc où elles sont déclarées. Pour le code parent, il n'y a pas de variable.
En solution, on peut envisager de déclarer la variable dans le bloc parent et de la modifier ensuite :

```jsx
let userLoggedIn = true;
let welcomeMessage = ''; // déclarer la variable ici

if (userLoggedIn) {
welcomeMessage = 'Welcome back!'; // modifier la variable extérieure
} else {
welcomeMessage = 'Welcome new user!'; // modifier la variable extérieure
}

console.log(welcomeMessage); // imprime 'Welcome back!'
```

## Les instructions switch
Pour vérifier la valeur d'une variable par rapport à une liste de valeurs attendues et réagir en conséquence.
Supposons que l'on ait plusieurs objets utilisateurs, et que je souhaite vérifier le type de compte de chacun pour envoyer un message personnalisé :

```jsx
let firstUser = {
name: "Will Alexander",
age: 33,
accountLevel: "normal"
};

let secondUser = {
name: "Sarah Kate",
age: 21,
accountLevel: "premium"
};

let thirdUser = {
name: "Audrey Simon",
age: 27,
accountLevel: "mega-premium"
};
```

L'instruction switch va prendre la variable à vérifier et une liste de valeurs

```jsx
switch (firstUser.accountLevel) {
case 'normal':
      console.log('You have a normal account!');

break;
case 'premium':
      console.log('You have a premium account!');

break;
case 'mega-premium':
      console.log('You have a mega premium account!');
break;

default:
      console.log('Unknown account type!');
}
```

-   case : code à exécuter dans chaque instruction
-   break : permet de stopper l'exécution des cas suivants (en cascade)
-   default : ne sera exécuté que si la variable que l'on vérifie ne correspond à aucune des valeurs répertoriées

# Utilisez la bonne boucle pour répéter les tâches
Certaines instructions doivent être répétées plusieurs fois, pour ces cas nous utilisons les boucles.

## La boucle for
Elle permet de savoir "combien de fois"

Si je veux faire embarquer 10 passagers, sans accorder d'importance à l'ordre d'embarquement, j'utilise une boucle for pour les embarquer un par un jusqu'à atteindre 10. La variable d'indice i sert de compteur pour le nombre d'execution de la boucle. La deuxième condition est la condition de poursuite de la boucle : dès qu'elle s'évalue comme false on quitte la boucle. Enfin la troisième commande permet d'incrémenter i (ajouter 1) à chaque exécution. C'est ce qui permet de suivre le nombre d'exécution de la boucle.

Dans ce cas, on veut l'exécuter autant de fois qu'il y a de passagers donc quand i atteint 10 (après 10 boucles), on souhaite l'arrêter.

```jsx
const numberOfPassengers = 10;
for (let i = 0; i < numberOfPassengers; i++) {
   console.log("Passager embarqué !");
}
```

## Travaillez sur des tableaux : for ... of et for ... in
Lorsque j'ai un tableau et que je dois le parcourir
### La boucle for ... in
Très comparable à for mais plus facile à lire et effectue le travail d'itération pour moi.

```jsx
const passengers = [
"Will Alexander",
"Sarah Kate'",
"Audrey Simon",
"Tao Perkington"
]

for (let i in passengers) {
   console.log("Embarquement du passager " + passengers[i]);
}
```

i démarre automatiquement à zéro et s'incrémente à chaque boucle.

### La boucle for ... of
Lorsque l'indice précis d'un élément n'est pas nécessaire pendant l'itération, on utilise for ... of

```jsx
const passengers = [
"Will Alexander",
"Sarah Kate",
"Audrey Simon",
"Tao Perkington"
]

for (let passenger of passengers) {
   console.log("Embarquement du passager " + passenger);
}
```

Cela produit exactement le même résultat mais de façon plus lisible car on ne s'inquiète plus des indices et des tableaux. On reçoit simplement chaque élément dans l'ordre. C'est encore plus utile si le tableau est plus complexe et contient par exemple des objets :

```jsx
const passengers = [
{
name: "Will Alexander",
ticketNumber: 209542
},

{
name: "Sarah Kate",
ticketNumber: 169336
},

{
name: "Audrey Simon",
ticketNumber: 779042
},

{
name: "Tao Perkington",
ticketNumber: 703911
}
]

for (let passenger of passengers) {
   console.log('Embarquement du passager ' + passenger.name + ' avec le ticket numéro ' + passenger.ticketNumber);
}
```

## La boucle while
Elle vérifie si une condition est vraie. Si c'est le cas elle se poursuit, sinon elle s'arrête.

```jsx
let seatsLeft = 10;
let passengersStillToBoard = 8;
let passengersBoarded = 0;

while (seatsLeft > 0 && passengersStillToBoard > 0) {
passengersBoarded++; // un passager embarque
passengersStillToBoard--; // donc il y a un passager de moins à embarquer
seatsLeft--; // et un siège de moins
}

console.log(passengersBoarded); // imprime 8, car il y a 8 passagers pour 10 sièges
```

Cette boucle while poursuit son exécution jusqu'à ce que l'un des nombres seatsLeft et passengersStillTaBoard atteigne zéro. A ce point elle se termine.

# Gérez des erreurs et des exceptions dans mon programme
Ne pas faire d'erreur lorsqu'on code est pratiquement impossible. On distingue trois types d'erreurs

## Les erreurs de syntaxe
ou erreur d'analyse.
Elles surviennent quand je fais une faute d'écriture dans mon code. Il peut s'agir de l'oubli ou ajout d'un crochet, d'une faute d'ortographe ... Beaucoup d'éditeurs de texte mettent automatiquement en évidence les erreurs de syntaxe/

## Les erreurs de logique
-   affectation d'une valeur erronnée à une variable
-   mélange de conditions dans les instructions if
-   ordre incorrect d'écriture des lignes ou des blocs de code

Avec ce genre d'erreur mon programme peut avoir un comportement inattendu voire complètement planter.

## Les erreurs d'exécutions
Elles surviennent quand quelque chose d'inattendu se produit dans mon application. Il s'agit souvent de quelque chose associée aux ressources extérieures ou à une saisie/erreur humaine.

Parfois, on sait à l'avance que ce type d'erreur est susceptible de survenir, on peut prévoiri du code de traitement d'erreur. Une façon de traiter les erreurs potentielles consiste à utiliser une instruction if/else pour vérifier la validité des données.

```jsx
if (dataExists && dataIsValid) {
// utiliser les données ici
} else {
// gérer l'erreur ici
}
```

On peut aussi utiliser des blocs try/catch

```jsx
try {
// code susceptible à l'erreur ici
} catch (error) {
// réaction aux erreurs ici
}
```

# Travaillez sur les fonctions
## Comprendre les fonctions
Une fonction est un bloc de code auquel j'attribue un nom. Quand j'appelle cette fonction, elle exécute le code qu'elle contient. Par exemple console.log() permet d'imprimer sur la console.

```jsx
// On définit la fonction

function afficherDeuxValeurs(valeur1, valeur2) {
      console.log('Première valeur:' + valeur1);
      console.log('Deuxième valeur:' + valeur2);
}

// On exécute la fonction
afficherDeuxValeurs(12, 'Bonjour');

// On obtient dans la console
// > Première valeur:12 
// > Deuxième valeur:Bonjour
```

Quand je déclare une fonction, j'indique la liste des variables dont elle a besoin pour effectuer son travail : je définis les paramètres de la fonction.

A l'appel de la fonction, je lui attribue des valeurs pour ses paramètres. Les valeurs sont les arguments d'appel.

Ma fonction peut donner un résultat : une valeur de retour.

Si j'ai un fonction qui compte le nombre de mots dans une chaine :

-   le paramètre sera une chaine dont je vais compter les mots
-   l'argument sera toute chaine attribuée à une fonction quand je l'appelle
-   la valeur de retour sera le nombre de mots

# Définir des méthodes d'instance et des propriétés
Propriété de classe = attribut de classe
C'est une variable interne à une classe que l'on peut définir par défaut et faire évoluer au fur et à mesure du code. On peut ensuite exploiter ces propriétés pour afficher leurs valeurs, les utiliser pour des calculs, les modifier, etc.

## Tirez parti des classes avec des méthodes d'instance
On peut ajouter des méthodes d'instance aux classes, pour augmenter leur puissance et leur utilité.

Une méthode d'instance est une fonction faisant partie d'une classe, et qui agit sur cette instance de classe.

Une instance de classe est un objet, c'est un type par référence donc je peux lui apporter des modifications. La partie constante désigne une référence à cette instance mais n'est pas bloquante.

```jsx
class BankAccount {
   constructor(owner, balance) {
      this.owner = owner;
      this.balance = balance;
   }
}
```

On peut ensuite créer une instance de cette classe appelée newAccount

```jsx
const newAccount = new BankAccount("Will Alexander", 500);
```

Telle quelle, l'instance n'est pas très utile. Je peux lui ajouter une mise en forme en ajoutant une méthode à la classe :

```jsx
class BankAccount {
	constructor(owner, balance) {
		this.owner = owner;
		this.balance = balance;
}
	showBalance() {
		console.log("Solde: " + this.balance +" EUR");
	}
}
```

Je peux utiliser la notation dot sur l'instance, pour appeler sa méthode.
Je peux aussi ajouter des méthodes capable de modifier les propriétés de l'instance

```jsx
class BankAccount {
constructor(owner, balance) {
this.owner = owner;
this.balance = balance;
}

showBalance() {
      console.log("Solde: " + this.balance + " EUR");
}

deposit(amount) {
      console.log("Dépôt de " + amount + " EUR");
this.balance += amount;
this.showBalance();
}

withdraw(amount) {
if (amount > this.balance) {
         console.log("Retrait refusé !");
} else {
         console.log("Retrait de " + amount + " EUR");
this.balance -= amount;
this.showBalance();
}
}
}
```

Dans le corps d'une classe, this fait référence à l'instance créée de la classe.

## Découvrir les méthodes statiques
Elle est différente des méthodes d'instance car elle n'est pas liée à une instance particulière, mais à la classe elle-même. Elle sert à créer des méthodes utilitaires (= helper). Par exemple l'objet Math en Javascript contient beaucoup de méthodes utiles :

```jsx
const randomNumber = Math.random(); // crée un nombre aléatoire sur l'intervalle [0, 1]

const roundMeDown = Math.floor(495.966); // arrondit vers le bas à l'entier le plus proche, renvoie 495
```

Je n'ai pas besoin de créer par new une instance de l'objet, il suffit d'appeler l'objet Math global.

```jsx
class BePolite {
    
static sayHello() {
      console.log("Hello!");
}

static sayHelloTo(name) {
      console.log("Hello " + name + "!");
}

static add(firstNumber, secondNumber) {
return firstNumber + secondNumber;
}
}

BePolite.sayHello(); // imprime "Hello!""

BePolite.sayHelloTo("Will"); // imprime "Hello Will!""

const sum = BePolite.add(2, 3); // sum = 5
```

## C'est quoi le DOM ?
DOM = Document Objet Model, c'est une interface de programmation qui représente une page HTML permettant d'accéder à ses éléments et de les modifier avec Javascript.

Chaque élément de notre DOM est un objet Javascript avec ses propriétés et fonctions pour le manipuler. On doit d'abord retrouver des éléments eu sein de notre page HTML :

### Recherches depuis le document

```jsx
const element = document.getElementById("mon-ancre");
const element = document.getElementsByClassName("ma-classe");
const element = document.getElementsByTagName("div"); 
const element = document.querySelector("mon-ancre p.article > a" /// fera une recherche dans l'élément ayant pour id  #myId , les éléments de type  <p>  qui ont pour classe  article , afin de récupérer le lien (  <a>  ) qui est un enfant direct (pas des enfants de ses enfants).
```

### Recherches depuis un élément

```jsx
element.children();
element.parentElement();
element.nextElementSibling();
element.previousElementSibling();
```

## Modifier les éléments du DOM
### Créez le contenu d'un élément

Définir une valeur à innerHTML ou textContent remplace directement le contenu actuel de l'élément par celui que vous précisez.

```jsx
let elt = document.getElementById('main');
elt.innerHTML = "<ul><li>Elément 1</li><li>Elément 2</li></ul>";
```

innerHTML permet d'ajouter des éléments au sein d'une page HTML (à éviter pour du texte brut, rique de sécurité) :

[element.innerHTML](https://developer.mozilla.org/fr/docs/Web/API/Element/innerHTML)

textContent permet d'ajouter du texte :

[element.textContent](https://developer.mozilla.org/fr/docs/Web/API/Node/textContent)

### Modifiez des classes

```jsx
elt.classList.add("nouvelleClasse");    // Ajoute la classe nouvelleClasse à l'élément
elt.classList.remove("nouvelleClasse"); // Supprime la classe nouvelleClasse que l'on venait d'ajouter
elt.classList.contains("nouvelleClasse");   // Retournera false car on vient de la supprimer
elt.classList.replace("oldClass", "newClass"): // Remplacera oldClass par newClass si oldClass était présente sur l'élément
```

### Changez le style

```jsx
elt.style.color = "#fff";      // Change la couleur du texte de l'élément en blanc
elt.style.backgroundColor = "#000"; // Change la couleur de fond de l'élément en noir
elt.style.fontWeight = "bold"; // Met le texte de l'élément en gras
```

[HTMLElement.style](https://developer.mozilla.org/fr/docs/Web/API/ElementCSSInlineStyle/style)

### Modifiez les attributs

```jsx
elt.setAttribute("type", "password");   // Change le type de l'input en un type password
elt.setAttribute("name", "my-password");    // Change le nom de l'input en my-password
elt.getAttribute("name");               // Retourne my-password
```

[Element.setAttribute()](https://developer.mozilla.org/fr/docs/Web/API/Element/setAttribute)

### Créez des éléments

```jsx
const newElt = document.createElement("div");
```

Un élément créé avec cette fonction ne fait pas encore partie du document, il n'apparait donc pas sur la page. Pour le voir, il va d'abord falloir l'ajouter en tant qu'enfant à un élément.

[document.createElement](https://developer.mozilla.org/fr/docs/Web/API/Document/createElement)

### Ajoutez des enfants

```jsx
const newElt = document.createElement("div");
let elt = document.getElementById("main");

elt.appendChild(newElt);
```

### Supprimez et remplacez des éléments

```jsx
const newElt = document.createElement("div");
let elt = document.getElementById("main");
elt.appendChild(newElt);

elt.removeChild(newElt); // Supprime l'élément newElt de l'élément elt
elt.replaceChild(document.createElement("article"), newElt); // Remplace l'élément newElt par un nouvel élément de type article
```

[element.replaceChild](https://developer.mozilla.org/fr/docs/Web/API/Node/replaceChild)

[element.removeChild](https://developer.mozilla.org/fr/docs/Web/API/Node/removeChild)

## Ecoutez des événements

Un événement est une réaction à une action émise par l'utilisateur. En JavaScript c'est représenté par un nom ( click , mousemove ...) et une fonction que l'on nomme une callback.
Pour écouter un événement : addEventListener()
Type d'événements :
[Référence des événements](https://developer.mozilla.org/fr/docs/Web/Events)

### Réaction à un clic
```jsx
const elt = document.getElementById('mon-lien'); // On récupère l'élément sur lequel on veut détecter le clic
elt.addEventListener('click', function() { // On écoute l'événement click
    elt.textContent = "C'est cliqué !"; // On change le contenu de notre élément pour afficher "C'est cliqué !"
});
```

```jsx
const elt = document.getElementById('mon-lien'); // On récupère l'élément sur lequel on veut détecter le clic
elt.addEventListener('click', function(event) { // On écoute l'événement click, notre callback prend un paramètre que nous avons appelé event ici
    event.preventDefault(); // On utilise la fonction preventDefault de notre objet event pour empêcher le comportement par défaut de cet élément lors du clic de la souris
});
```

Par défaut, l'événement est propagé aux éléments parents. Pour éviter cela, on utilise :

```jsx
elementInterieur.addEventListener('click', function(event) {
    event.stopPropagation();
    elementAvecMessage.innerHTML = "Message de l'élément intérieur";
});
```