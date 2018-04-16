# Evénéments

## Ecouter un événement

Angular propose un mécanisme d'écoute d'événements avec la syntaxe suivante :

```html
(evenement)="expression"
```

Exemple :

```ts
import { Component } from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<button (click)="quandOnClique()">Clic</button>`
})
export class MonComposant {

    quandOnClique() {
        console.log("Mr l'utilisateur, vous venez de cliquer");
    }

}
```

Une expression peut :
* invoquer des méthodes `quandOnClique()`
* effectuer des affectations `nom ='Thierry'`
* effectuer plusieurs instructions `nom = 'Thierry';prenom='Bougo'`

## Objet `$event`

Pour accéder à l'objet événement, utiliser la variable `$event`.

```ts
import { Component } from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<button (click)="quandOnClique($event)">Clic</button>`
})
export class MonComposant {

    quandOnClique(event) {
        console.log("objet événement", event);

    }
}
```

## Evénément du clavier

Angular fournit un support des événements du clavier via des événements `keydown.*`.

Exemple d'événement :

* `keydown.space`
* `keydown.alt.space`
* ...

Exemple :

```ts
import {Component} from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<button (keydown.space)=“onClick()">Clic</button>`
})
export class MonComposant {

    onClick() {
        alert("tu as cliqué sur espace");
    }
}
```