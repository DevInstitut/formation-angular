# Gestion des liens

La directive `RouterLink` placée sur un lien permet de préciser une ancre indépendamment du mode (hashbang ou html5).


```html
<header> <!-- Entête --></header>
<nav>

   <!-- définition d'un lien basé sur les routes. -->
   <a routerLink="/page1">Page 1</a>
   <a routerLink="/page2">Page 2</a>

</nav>
<div id="content">
    <router-outlet></router-outlet>
</div>
<footer><!-- Pied de page --></footer>
```

La directive `RouterLinkActive` permet de positionner une classe CSS lorsque la route courante correspond à la valeur de l'attribut `routerLink`.

```html

<nav>
    <!-- la classe CSS active-link est ajouté à l'élément lorsque la route désignée est active -->
   <a routerLink="/page1" routerLinkActive="active-link">Page 1</a> <1>
   <a routerLink="/page2" routerLinkActive="active-link">Page 2</a>
</nav>
```

