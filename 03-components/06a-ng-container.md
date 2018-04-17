# ng-container

La balise `<ng-container>` permet de grouper des éléments sans interférer avec le DOM.

Exemple :

```html
<p>
    Cette action est
    <ng-container *ngIf="decisif">décisive et</ng-container>
    importante.
</p>
```

Si `decisif` vaut `true` alors le résultat sera :

```html
<p>
    Cette action est
    décisive et
    importante.
</p>
```

Noter ici la disparition de la balise `<ng-container>`.