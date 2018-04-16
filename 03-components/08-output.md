# @Output

Le décorateur `@Output` permet à un composant d'émettre un événement personnalisé.

Exemple :

```ts
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `<button (click)="quandOnClique()">Clic</button>`
})
export class MonComposant {

    @Output() change:EventEmitter<string> = new EventEmitter<string>();

    quandOnClique() {
        this.change.emit('du nouveau')
    }
}
```

A l'utilisation :

```html
<!-- $event vaudra 'du nouveau' -->
<mon-composant (change)="traiter($event)"><mon-composant>
```