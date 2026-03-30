# La technologie SCSS

## SCSS ? C'est quoi ?

Le **SCSS** est une technologie dévelopée dans le but de **simplifier et d'accélerer** le codage CSS d'un développeur, ainsi que de **le personnaliser et de donner une structure plus propre** au CSS final.
___

## Installation SCSS

Afin de pouvoir installer le SCSS, nous avons besoin du packet manager **npx** que l'on peut trouver sur internet, il n'est pas nécessaire de l'installer pour chaque projet une fois suffit.

Ensuite, il faut taper dans la ligne de commande à la localisation de ton projet la commande suivante.

```bash
Documents/Ton-Projet$ npm install sass
```

Et maintenant tu auras accès sur ton projet à toute la technologie **SCSS**.
## Syntaxe SCSS

La syntaxe SCSS se rapproche fortement de la syntaxe **CSS classique**

```scss
h1 {
    background-color:#000000;
}
.myClass {
    color:#ffffff;
}
#myId {
    font-size:24px;
}

```
La plus grosse différence vient des fonctionnalité de **rangement** qu'elle rajoute, notamment la possibilité **d'imbriquer le SCSS** tel que:
```scss
.myCard {
    background-color:#ffffff;
    .card-title {
        font-size:24px;
    }
}
```

> **Le rendu en CSS sera:**

```css
.myCard{
background-color:#ffffff;
}
.myCard .card-title {
    font-size:24px;
}
```

___

## Methode BEM
Le SCSS nous permet de ranger notre code de façon plus efficaces et moins lourdes en lecture grace nottament à la **méthode BEM**, qui est une convention de nomage permettant de grandement réduire la taille de ce que l'on écrit dans le SCSS.

Prenons par exemple ce **code HTML**

```html
<div class="myclass">
    <div class="myclass__layer1">
        <div class="myclass__layer1__bloc1">
        </div>
        <div class="myclass__layer1__bloc2">
        </div>
    </div>
    <div class="myclass__layer2">
        <div class="myclass__layer2__bloc1">
        </div>
        <div class="myclass__layer2__bloc2">
        </div>
    </div>
</div>
```

En CSS afin de cibler chacune de ces classes individuellement, il faudrait écrire à rallonge chacun des noms de classes.

Cependant avec le SCSS, nous pouvons énormément **raccourcir** le code que l'on doit écrire pour le même cas de figure


```scss
.myclass{
    &__layer1{
        &__bloc1{
        }
        &__bloc2{
        }
    }
    &__layer2{
        &__bloc1{
        }
        &__bloc2{ 
        }
    }
}
```

> Le code ci-dessus permettra de cibler individuellement **chacune des classes** du HTML sans avoir à toutes les réecrire une à une.
___
## Les Variables SCSS
___
## Les Mixins
**Les mixins** sont un outil SCSS qui nous permet de réutiliser du code à **plusieurs endroits** dans nos fichier.

```scss
@mixin myMixin {
    background-color:#000000;
    color:#ffffff;
}
.myClass{
    @include myMixin;
    border-radius:4px;
}
```

**Traduction CSS**

```css
.myClass{
    background-color:#000000;
    color:#ffffff;
    border-radius:4px;  
}
```

Les Mixins nous permettent également de faire des media-queries de façon propre et standardisé dans le code.

```scss
@mixin sm {
  @media (max-width: 640px) {
    @content;
  }
}
.myClass{
    padding: 4rem;
    margin: 1rem;

    @include sm {
        padding:2rem 0;
        margin:0;
    }
}
```

 > **Le code écrit dans le ```@include``` sera utilisé seulement-si la taille de l'écran est inférieur à 640px**
___
## Les Lists et Maps

Les lists et maps sont deux types de **Collections de données** les lists s'apparentes à des **array** dans un language classique et les maps à un **dictionnaire** dans un language classique.

```scss
// Une List
$tailles: 0.5rem, 1rem, 2rem, 2.5rem;

// Un Map
$couleurs:(
  'background': #192a36,
  'text': #dedede,
);
```

Afin de récupérer les données quelles contiennent, nous utilisons différentes méthodes.

### Pour Une List:

```scss
$tailles: 0.5rem, 1rem, 2rem, 2.5rem;

$premiere: nth($tailles, 1); 
// nous permet d'acceder au 1er index de la liste, ici 0.5rem

$longueur: length($tailles); 
// nous donnes la longueurs de la list, ici 4.
```

### Pour Un Map:

```scss 
$couleurs:(
  'background': #192a36,
  'text': #dedede,
);

$color--text: map-get($couleurs, "text")
/* $color--text est maintenant de la valeur #dedede */
```

> **Les Lists et les Maps ne sont pas puissantes par elle-même, il faut les combiner avec notre prochain sujet pour les rendre vraiments utiles**

___
## Les Boucles

Les Boucles permettent de réexecuter une partie du code plusieurs fois.

Il y'en a plusieurs qui sont utiles pour différents cas de figure.

### La Boucle ```@for```

La boucle ```@for``` permet d'éxecuter du code un **nombre de fois prédeterminer** ou selon la taille d'une **list**.

```scss
@for $i from 1 through 4 {
    .col-#{$i} {
        width: 25% * $i;
  }
}

$tailles: 0.5rem, 1rem, 2rem, 2.5rem;

@for $i from 1 through length($tailles) {
    .font-size-#{$i} {
        font-size: nth($tailles, #{$i})
    }
}
```
> **Le rendu en CSS sera:**

```css
 .col-1 {
    width: 25%
 }
  .col-2 {
    width: 50%
 }
  .col-3 {
    width: 75%
 }
  .col-4 {
    width: 100%
 }

 .font-size-1 {
    font-size: 0.5rem
 }
  .font-size-2 {
    font-size: 1rem
 }
  .font-size-3 {
    font-size: 2rem
 }
  .font-size-4 {
    font-size: 2.5rem
 }
```
### La Boucle ```@each```

La boucle ```@each``` permet d'itérer sur chacun des élements d'une **list** ou d'un **map**.

```scss

$couleurs:(
  'black': #192a36,
  'white': #dedede,
  'green': #baff9f,
  'red': #ff9797,
);

@each $nom,$couleur in $couleurs {
  .texte-#{$nom} {
    color: $couleur;
  }
}
```
> **Le rendu en CSS sera:**

```css
.texte-black{
    color:#192a36
}
.texte-white{
    color:#dedede
}
.texte-green{
    color:#baff9f
}
.texte-red{
    color:#ff9797
}
```

### La Boucle ```@while```

La boucle ```@while``` permet d'executer du code tant que la condition de sortie n'est pas remplie.

```scss
$i:1;

@while $i != 3 {
.font-#{$i} {
    font-size: 4px * $i
    }
    $i: $i + 1
}
```
___
## Les Fonctions SCSS
Les fonctions scss nous permettent de réaliser du code qui s'adaptent à ce que l'on met dedans.

```scss
@function rem($px) {
    @return $px / 16px * 1rem;
}

.myClass {
    font-size: rem(20);
// nous donnes l'equivalent de 20px en rem 
}
 ```

 