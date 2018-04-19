# Pipe personnalisé

Il est possible de créer ses propres pipes.

Exemple de Pipe :

```ts
import {PipeTransform, Pipe} from '@angular/core';

@Pipe({name: 'monPipe'})
export class MonPipe implements PipeTransform {
    transform(value, args) {
        return `${value} - c'est moi :)`;
    }
}
```

Exemple d'utilisation d'un Pipe dans un composant :

```ts

@Component({
    selector: 'mon-cmp',
    template: " <p>{{ mot | monPipe }}</p>",
    pipes: [MonPipe]
})
class TestCmp { mot: string = 'un mot '; }

```
 
 Ici la chaîne de caractères `'un mot'` sera transformée en `'un mot - c'est moi :)'`.