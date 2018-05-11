# Créer un service

## Exemple de service

```ts
import {Injectable} from '@angular/core';

@Injectable()
export class PersonneService {

  // injection d'un service
  constructor(private _autreService:AutreService) {}

  list() { // ...}
}
```

Le décorateur `@Injectable` n'est pas obligatoire, il est requis dans le cas où l'on souhaite injecter un autre service.

## Rendre disponible un service au sein d'un module

```ts
// ...
import { PersonneService } from './shared/service/personne.service';

@NgModule({
  //...
  providers: [PersonneService],
  // ...
})
export class AppModule { }
```

> Depuis Angular 6, un attribut `providedIn` a été ajouté au décorateur @Injectable(). Celui-ci rend optionnel, la déclaration du service dans le module. Exemple :

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class PersonneService {
  constructor() { }
}
```


## Utiliser un service dans un composant

```js
@Component({ // ...})
export class MonComposant {

  // injection du service
  constructor(private pService:PersonneService) {
  }

  list() {
    // utilisation du service
    this.pService.list()
  }
}
```
