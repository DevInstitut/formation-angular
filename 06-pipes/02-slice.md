# Slice

* Permet de n'afficher qu'un sous-ensemble d'une collection.

* Fonctionne comme la méthode [slice JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/slice) : slide (indice_depart, indice_fin). L'indice de fin est optionnel.

* Fonctionne également avec des chaines de caractères

```html
<p>{{ personnes | slice:0:2 }}</p>
<p>{{ 'texte' | slice:0:2 }}</p>
<p>{{ 'texte' | slice:2 }}</p>
<p>{{ 'texte' | slice:-2 }}</p>
<div *ngFor="#p of personnes | slice:0:2">
<div *ngFor="#p of personnes | slice:0:size">
```





