## Subject

```js

// Angular 5
// import {Observable} from 'rxjs/Observable';
// import 'rxjs/add/observable/interval';
// import {Subject} from "rxjs/Subject";

// Angular 6
import {Observable, Subject, interval} from 'rxjs';

// Soit une source
var source = Observable.interval(1000);

// Un Subject est à la fois un Observable et un Observateur

// Créer un Subject
var subject = new Subject();

// Subject en tant qu'abonné
source.subscribe(subject);

// Ajouter un observateur
subject.subscribe(value => console.log(value));

// Il donne la possibilité d'emettre une nouvelle valeur après sa construction
subject.next('foo');

// foo
// 1
// 2
// ...

```

## Catégories de Subject

* `Subject` : ne stocke aucune valeur.

* `ReplaySubject` : stocke toutes les valeurs publiées. Dès qu'un observateur s'abonne, il reçoit l'intégralité de l'historique.

* `BehaviorSubject` : il est similaire au ReplaySubject à la différence qu'il ne stocke que la dernière valeur.

* `AsyncSubject` : stocke uniquement la dernière valeur mais ne publie aux observateurs qu'une fois le flux terminé.

## Exemple Subject

```js
const subject1 = new Subject()

subject1.next(1)
subject1.next(2)

subject1.subscribe(val => console.log(val))

subject1.next(3)

subject1.complete()

// 3

```

## Exemple ReplaySubject

```js
const subject1 = new ReplaySubject()

subject1.next(1)
subject1.next(2)

subject1.subscribe(val => console.log(val))

subject1.next(3)
subject1.complete()

// 1
// 2
// 3
```

## Exemple BehaviorSubject

```js
const subject1 = new BehaviorSubject(0)

subject1.next(1)
subject1.next(2)

subject1.subscribe(val => console.log(val))

subject1.next(3)

subject1.complete()

// 2
// 3

```

## Exemple AsyncSubject

```js
const subject1 = new AsyncSubject()

subject1.next(1)
subject1.next(2)

subject1.subscribe(val => console.log(val))

subject1.next(3)
subject1.next(4)

subject1.complete()

// 4
```

## Exemple de mise en oeuvre dans Angular


Soit un service `ServiceA` qui fait un traitement :

```ts

@Injectable()
export class ServiceA {

    faitUneAction(data:string) {
    
    }
}
```

Ce service est appelé par le composant `Composant1` lors d'un événement.


```ts
// ...
export class Composant1 {
    
    constructor(private _srvA: ServiceA) {
        
    }
    
    lorsDUnEvenement(valeur:string) {
        this._srvA.faitUneAction(valeur);
    }
}
```

> La problématique : nous avons le composant `Composant2` affiché en même temps que le composant `Composant1`
qui doit se mettre à jour à chaque fois qu'une action est déclenchée (`ServiceA.faitUneAction(valeur)`).

Nous pouvons pour cela, créer un objet `Subject` permettant de gérer la propagation de l'information entre des composants.

* Etape 1 : Mise à jour du service

```ts
import {Subject} from "rxjs/Subject";

@Injectable()
export class ServiceA {
    
    // création d'une instance de Subject
    // le subject est privé, seul le service ServiceA peut émettre une valeur
    // <string> désigne la nature de la donnée à notifier
    private action = new Subject<string>();
    
    // création d'une propriété publique
    // accessible en dehors du service
    // seule l'interface Observable du Subject est exposée
    get actionObs() {
        this.action.asObservable();
    }

    faitUneAction(data:string) {
        // exécution de l'action
        
        // notification de tous les observateurs avec la donnée courante
        this.action.next(data);
    }
}
```

* Etape 2 : Abonnement du composant `Composant2`

```ts

// ...
export class Composant2 implements OnDestroy {

    actionSub:Subscription
    
    constructor(private _srvA: ServiceA) {
        
         // abonnement du composant aux notifications
        this.actionSub = this._srvA.actionObs.subscribe(
        (data:string) => {
        
            // donnée propagée par le service via next(data)
        
        },
        error => {
            // signal d'erreur
        },
        
        () => {
        // signal de fin
        });    
    }
    
    ngOnDestroy() {
        // désabonnement du composant avant sa destruction
        this.actionSub.unsubscribe();      
    }
    
    
}
```



