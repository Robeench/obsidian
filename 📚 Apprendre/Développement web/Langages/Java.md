[[Langage]]
# Java
## Déclaration de variable
Pour créer une variable, il faut la déclarer. Il existe plusieurs types de variables en Java.
Les variables contenant des nombres entiers sont déclarées en utilisant `int`, par exemple :

```java
int ongoingAllowance = 500;
int savings = 1000;
```

Ici on a déclaré deux variables, et assignée une valeur initiale à celles-ci.

Pour déclarer des nombres décimaux (avec virgule), on utilise le type `double`

## Modifier la valeur d'une variable avec les opérations

Une variable peut changer de valeur. Pour la faire varier, on peut effectuer plusieurs opérations.

Chaque opération fonctionne grâce à des opérateurs arithmétiques :

-   `+` addition
-   `-` soustraction
-   `*` multiplication
-   `/` division

Les règles arithmétiques s'appliquent, notamment l'ordre d'exécution. On peut utiliser les parenthèses pour décider de cet ordre.

Une affectation assigne une valeur à une variable :

`nomDeLaVariable` (_nom_ de la variable) `=` (_opérateur d'affectation_) `affectationQuiProduitUneValeur` (expression produisant une valeur égale au _type_ de la variable)

### Opérateur d'affectation raccourci

```java
savings = 10000;

savings = savings + 100;
// version raccourcie
savings += 100;
```

L'opérateur d'affectation peut se joindre à l'opérateur arithmétique

Autres variantes courtes :

-   `+=` addition
-   `-=` soustraction
-   `*=` multiplication
-   `/=` division

## Les différents types

-   `string` : texte
-   `int` : nombre entier
-   `double` : nombre décimal

```java
String text = "A wonderful string that consists of multiple characters"
int numberOfVowels = 0
double percentageOfVowels = 0.0
```

### Les constantes

Elles sont utiles car :

-   elles permettent au programme d'être plus rapide. L'ordinateur sait quel espace la constante prend et il n'a pas besoin de vérifier les valeurs alternatives lors des opérations.
-   Vérifiez que certaines valeurs ne changent pas, intentionnellement ou par accident. Par exemple on ne veut pas modifier les jours de la semaine ou le nombre de jours dans une année.

<aside> 💡 Il est recommandé d'utiliser des constantes dans la mesure du possible.

</aside>

`final` : permet de déclarer une constante

```java
final int numberOfWeekdays = 7;
final String myFavouriteFood = "Icecream";

int numberOfPets = 1;
String currentSeason = "Winter";
```

# Choisir le bon type d'une variable

## Utilité d'un type de données

Selon ce que l'on souhaite mettre dans une variable, on peut utiliser des types différents. En fonction, nous définissons comment elle pourra être manipulée, et comment son contenu pourra être utilisée.

L'unique façon de déclarer une variable est de spécifier directement son type.

![https://user.oc-static.com/upload/2019/09/26/15695035079543_VISUELS-SARAH-01 copie.png](https://user.oc-static.com/upload/2019/09/26/15695035079543_VISUELS-SARAH-01%20copie.png)

Il faut commencer par le type, puis le nom, puis la valeur. Si on n'a pas tout de suite de valeur à assigner à sa variable, il faut quand même lui définir un type. Par contre, elle ne sera pas utilisable tant que sa valeur ne lui aura pas été attribuée.

Pendant l'exécution de mon programme, mon CPU (unité centrale de traitement) doit savoir combien d'espace réserver à ma variable. Le type permet d'allouer un espace mémoire adapté.

Parmi les types, il existe les types primitifs, ils existent par eux-mêmes, par exemple les types numériques et les chaines.

Les types les plus simples servent de base pour toutes les opérations informatiques. Il est possible de les combiner pour construire des types plus complexes.

## Les types numériques

### Les entiers

Ils sont déclarés comme n'importe quelle autre variable.

```java
int count = 10;
```

### Les décimales

Pour les décimales, on utilise deux types différents :

-   `float` : permet de préciser jusqu'à 7 décimales après la virgule
-   `double` : permet de stocker la totalité d'un nombre décimale, sans limite après la virgule

Il faut privilégier `float` dès que possible, afin de ne pas gaspiller de mémoire.

```java
double a = 1876.79797657765609870978709780987;
float b = 1876.79797657765609870978709780987;
// elles perdent de la précision, mais pas au même niveau 
// a -> 1876.797976
// b -> 1876.79
```

## Mélangez les types numériques

Dans chaque programme, on peut être amenée à faire des opérations mathématiques, mais les variables utilisées ne sont pas forcément du même type.

Par exemple, une division entre deux entiers s'appelle une division entière. Elle a toujours pour résultat un nombre entier. Donc le code suivant donne 2 :

```java
int a = 10;
int b = 4;
double c = a/b;
```

Pour obtenir un résultat avec une décimale, il faut combiner deux types :

```java
int a = 10;
int b = 4;
double c = a/(double) b; //-> c contient 2.5, car la valeur de b est transformée en double
```

On peut faire en sorte qu'une variable d'un type agisse comme un autre type. C'est ce qu'on appelle le _type casting_ : `(double)b`

## Les strings

Permet de stocker du texte, soit une chaine de caractères.

```java
String city = "New York";
```

On peut :

-   fusionner plusieurs string
-   concaténer : mettre bout à bout des string et des variables (avec des types de données textes ou numériques)

```java
**String favoriteCity = "Buenos Aires";
int numberOfTrips = 5;

String story = "I've traveled to " +favoriteCity+ " " +numberOfTrips+ " times!"; // -> "I've traveled to Buenos Aires 5 times!"**
```

# La fonction principale

Les fonctions permettent de réaliser certaines tâches spécifiques du programme et seront appelés autant de fois que nécessaire. En écrivant le code, on attribue un nom au bloc de code correspondant à la fonction. Pour exécuter ce bloc de code, il suffit de le mentionner par son nom : soit _appeler une fonction_.

Lorsque l'on exécute un programme, il sait par où commencer. En effet, quelque soit le langage de programmation, il y a toujours une fonction prinicipale. Elle est déclenchée en premier et le programme exécute ses instructions. Le code de cette fonction principale va faire appel à d'autres fonctions, à l'intérieur.

Dans certains langages, cette fonction est directement visible pour le développeur. Pour d'autres langages, elle est masquée pour le développeur.

En Java, on y accède en écrivant un code que l'on lance manuellement. Mais dans le cadre d'une véritable application, elle sera masquée par les librairies que le développeur utilise.

## Hello World !

```java
package hello;
/** Ceci est une implémentation du message traditionnel "Hello world!"
* @author L'équipe Education d'OpenClassrooms
*/
public class HelloWorld {
/** Le programme commence ici */
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

-   `package hello;` : permet d'utiliser Hello
-   `public class HelloWorld {` : définit le nom de la classe comme HelloWorld
-   `public static void main(String[] args)` : à l'intérieur de la classe, on trouve la déclaration de fonction. C'est le bloc de code que l'interpréteur Java recherche lorsque mon programme démarre
-   `System.out.println("Hello World !");` : à l'intérieur de la méthode principale, on trouve l'instruction qui affiche le message attendu

En résumé, le code de démarrage du programme est contenu dans une fonction _main_, elle même contenue dans une _classe_, elle-même appartenant à un _package_.

<aside> 💡 Le compilateur intervient en amont pour interpréter le code et le transformer en byteCode (ou code binaire). Puis l'interpréteur traduit le byteCode en instructions pour exécuter le programme.

</aside>

Les lignes dans les caractères `/**` et `*/` sont des commentaires de documentation. Cela crée un _Javadoc_ (une page web HTML) qui contient la documentation de mon code. Il est composé d'une liste de classes, de méthodes et de variables, ainsi que des commentaires. Il permet à d'autres développeurs d'utiliser mon code sans passer par le code Java actuel.

## Exécuter le programme à partir du terminal

Il y a une correspondance directe entre :

-   les packages et les dossiers
-   les classes et les fichiers

Pour exécuter le programme, il faut créer des dossiers correspondant à des packages et des fichiers correspondant aux classes.

Pour le moment mon code précédent est dans la méthode principale d'une classe `HelloWorld` et celle-ci se trouve dans un package `hello`. Mais ils ne correspondent pas pour le moment à des fichiers et dossiers.

1.  Créer un dossier dans lequel je mets tout mon code : il s'appelle le dossier root (racine)
2.  A l'intérieur du dossier root, créer un dossier hello correspondant au nom de mon package
3.  Créer un fichier [HelloWorld.java](http://helloworld.java), dans le dossier Hello, qui correspond au nom de ma classe

<aside> 💡 Soit package vers dossier, classe vers fichier

</aside>

Une fois le code à l'intérieur du fichier, il faut le rendre exécutable par une machine. Pour cela il doit être traduit en un ensemble d'instructions qu'un ordinateur peut exécuter. C'est le _code machine_. Pour Java, il est appelé _Bytecode_.

## Un code le plus compact possible

La fonction `main` est mon programe. Si je devais écrire toute la logique de mon programme à l'intérieur du main, cela donnerait une trop grande quantité de code à un seul endroit. Ce serait diificilement compréhensible et difficile à maintenir.

Il faut donc organiser son code en _classes_. Il existe deux types de classes :

### Classes de modèles

On les écrit pour modéliser le domaine de mon application, ce pour quoi j'écris mon programme.

Par exemple `String` qui est disponible dans le package `java.lang` .

`String` est une classe car son nom commence par une lettre majuscule et qu'il définit un état et un comportement :

-   état = chaine de caractères que l'on stocke. Valeur réelle définie pour chaque objet que l'on instancie.
-   comportement = ensemble des méthodes que la classe `String` définit et qui permettent d'opérer sur la chaine stockée.

Une classe permet donc d'accéder à des comportements prédéfinis. On les trouve tous au sein de la documentation :

[All Classes](https://docs.oracle.com/en/java/javase/11/docs/api/allclasses.html)

### Classes utilitaires

Elles contiennent des méthodes statiques qui peuvent être appelés directement sur la classe.

## Nettoyer la fonction main

<aside> 💡 Il ne faut rien garder dans ma fonction main qui puisse être extrait vers une fonction.

</aside>

Avec certains frameworks je n'aurais même pas accès à ma fonction main.

```java
package cleanHello;

/** Ceci est une implémentation du message traditionnel "Hello world!"
* @author L'équipe Education d'OpenClassrooms
*/
public class CleanWorld {

    /** Le programme commence ici */
    public static void main(String[] args) {
        sayHelloTo("world");
    }

    /** affiche le message "hello" au destinataire fourni
    *
    * @param recipient
    */
    private static void sayHelloTo(String recipient) {
        System.out.println("Hello " + recipient);
    }

}
```

-   `main` = point de départ du programme. Transmet le travail à la méthode `sayHelloTo` avec l'argument dont elle a besoin.
-   méthode `sayHelloTo` = imprime la chaine "Hello" et ajoute la valeur fournie à la variable destinataire `recipient` lorsqu'elle est appelée par la méthode `main`.