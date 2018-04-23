# Contrôle du flux d'exécution


```js
import {Observable} from 'rxjs/Observable';
import 'rxjs/add/observable/fromEvent';

// opérateur filter
import 'rxjs/add/operator/filter';

// opérateur map
import 'rxjs/add/operator/map';

const input = Observable.fromEvent(document.querySelector('input'), 'input');

// filtrer les saisies de moins de 3 caractères
input.filter(event => event.target.value.length > 2)
  .map(event => event.target.value)
  .subscribe(value => console.log(value));

```

En savoir plus sur les opérateurs : https://www.learnrxjs.io/operators/.

