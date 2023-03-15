# Java
## Déclaration de variable
Les variables contenant des nombres entiers sont déclarées en utilisant `int`, par exemple :

```java
int ongoingAllowance = 500;
int savings = 1000;
```

Pour déclarer des nombres décimaux (avec virgule), on utilise le type `double`

## Modifier la valeur d'une variable avec les opérations
-   `+` addition
-   `-` soustraction
-   `*` multiplication
-   `/` division

### Opérateur d'affectation raccourci
```java
savings = 10000;

savings = savings + 100;
// version raccourcie
savings += 100;
```

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

## Choisir le bon type d'une variable

### Utilité d'un type de données

Selon ce que l'on souhaite mettre dans une variable, on peut utiliser des types différents. En fonction, nous définissons comment elle pourra être manipulée, et comment son contenu pourra être utilisée.

L'unique façon de déclarer une variable est de spécifier directement son type.

![https://user.oc-static.com/upload/2019/09/26/15695035079543_VISUELS-SARAH-01 copie.png](https://user.oc-static.com/upload/2019/09/26/15695035079543_VISUELS-SARAH-01%20copie.png)

Il faut commencer par le type, puis le nom, puis la valeur. Si on n'a pas tout de suite de valeur à assigner à sa variable, il faut quand même lui définir un type. Par contre, elle ne sera pas utilisable tant que sa valeur ne lui aura pas été attribuée.

Pendant l'exécution de mon programme, mon [[CPU]] (unité centrale de traitement) doit savoir combien d'espace réserver à ma variable. Le type permet d'allouer un espace mémoire adapté.

Parmi les types, il existe les types primitifs, ils existent par eux-mêmes, par exemple les types numériques et les chaines.

Les types les plus simples servent de base pour toutes les opérations informatiques. Il est possible de les combiner pour construire des types plus complexes.

### Les types numériques

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

### Mélangez les types numériques

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

### Les strings

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
