# Observable

Dans RxJS, la structure utilisée pour représenter un flux de données asynchrones est **Observable<T>**.

Un Observable peut-être vu comme une promesse qui est capable de retourner plusieurs valeurs.


```ts

import {Observable} from 'rxjs/Observable'

// Créer un observable

//      next() permet d emettre une valeur
//      complete() permet de fermer l'observable
const observable$ = Observable.create(observer => {
    setTimeout(()=>  observer.next(1), 1000)
    setTimeout(()=>  observer.next(2), 2000)
    setTimeout(()=>  observer.complete(), 3000)
})

// Créer un Observateur
observable$.subscribe(
    value => console.log(value),
    error => console.log(error),
    () => console.log('terminé'))
    
// Résultat

// 1
// 2
// terminé
```

## Convertir en observable


* Depuis des valeurs :

```ts
import {Observable} from 'rxjs/Observable';

// import de l'opérateur Of
import 'rxjs/add/observable/of';

const obs$ = Observable.of('foo', 'bar');
```

* Dépuis un tableau

```ts
import {Observable} from 'rxjs/Observable';
import 'rxjs/add/observable/from';

const obs$ = Observable.from([1,2,3]);

```


* Depuis un événement

```ts
import {Observable} from 'rxjs/Observable';
import 'rxjs/add/observable/fromEvent';

const obs$ = Observable.fromEvent(document.querySelector('button'), 'click');

// Depuis une promesse
Observable.fromPromise(fetch('/users'));

```


* Depuis une promesse


```ts
import {Observable} from 'rxjs/Observable';
import 'rxjs/add/observable/fromPromise';

const obs$ = Observable.fromPromise(fetch('/users'));

```

## HTTP Client

Les requêtes HTTP envoyées via le client HTTP Angular retournent des résultats de type `Observable`.

```ts
// resultat$ est de type Observable
const resultat$ = this._http.get("https://jsonplaceholder.typicode.com/posts");
```