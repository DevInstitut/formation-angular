# Contrôle du flux d'exécution


```js
// Angular 5
// import {Observable} from 'rxjs/Observable';
// import 'rxjs/add/observable/fromEvent';

// Angular 6
import { Observable } from 'rxjs'
import { fromEvent } from 'rxjs';



// opérateur filter

// Angular 5
// import 'rxjs/add/operator/filter';

import { filter } from 'rxjs/operators';

// opérateur map

// Angular 5
// import 'rxjs/add/operator/map';
import { map } from 'rxjs/operators';

const input = Observable.fromEvent(document.querySelector('input'), 'input');

// filtrer les saisies de moins de 3 caractères

// Angular 5
// input.filter(event => event.target.value.length > 2)
//  .map(event => event.target.value)
//  .subscribe(value => console.log(value));

// Angular 6
input
    .pipe(
        filter(event => event.target.value.length > 2),
        map(event => event.target.value)
    ).subscribe(value => console.log(value));
```

En savoir plus sur les opérateurs : https://www.learnrxjs.io/operators/.

