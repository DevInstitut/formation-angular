# currency

* Permet de formater une somme d’argent dans une device donnée.

* Ses paramètres :
 * Le code ISO de la devise (EUR, USD, ...)
 * Un flag pour indiquer l’affichage du symbole (€, $, ...)
 * Une chaine de formatage du montant (même syntaxe que number)

```html

<p>{{ 10.6 | currency:'EUR' }}</p> <!-- affiche 'EUR10.6' -->

<p>{{ 10.6 | currency:'USD':true }}</p> <!-- affiche '$10.6' -->

<p>{{ 10.6 | currency:'USD':true:'.2' }}</p> <!-- affiche '$10.60' -->
```