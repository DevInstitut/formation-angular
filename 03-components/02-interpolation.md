# Interpolation

## Interpolation simple

Il est possible d'utiliser des variables dans le template via la syntaxe `{{maVariable}}`.

Exemple :

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'mon-composant',
  template: `<h1>Ceci est {{uneChose}} </h1>`
})
export class MonComposant {
  uneChose:string = 'UNE CHOSE'
}
```

La variable du template prendra la valeur d'une propriété de la classe du composant.

Si la propriété n’existe pas ou qu’elle vaut `undefined` (ou `null`), une chaine vide est affichée.

## Interpolation objet

Il est possible de référencer une propriété d'un objet.

```ts
import {Component} from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<h1>Nom = {{unObjet.nom}} </h1>`
})
export class MonComposant {
    unObjet:any = {nom:'Je suis', prenom: "Je n'en ai pas" }
}
```

Si la propriété de l'objet n'existe pas, Angular remonte une erreur et le template ne s'affiche pas.

Si l’objet utilisé dans le template peut être null, utiliser l’opérateur de navigation sûre (Safe Navigator Operator) : `?`.

`{{ monObjet?.propriete }}`

Exemple :

```ts
import {Component} from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<h1>Nom = {{unObjet?.nom}} </h1>`
})
export class MonComposant {
    unObjet:any = {nom:'Je suis', prenom: "Je n'en ai pas" }
}
```
