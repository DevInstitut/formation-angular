# async

* Affiche les données obtenues de manière asynchrone.

* Retourne une chaîne de caractères vide jusqu’à ce que les données deviennent disponibles (exemple: résolution de promesse). Un cycle de détection de changement est déclenché une fois la donnée obtenue.

```ts
import {Component} from ' @angular/core';

@Component({
    selector: 'mon-cmp',
    template: `<div>{{ donneeAsync | async }}</div>`
})
export class MonCmp {
    donneeAsync:Promise<string> = new Promise(resolve => {
        // promesse résolue après 1s
        window.setTimeout(() => resolve('bonjour async'), 1000);
    });
}
```