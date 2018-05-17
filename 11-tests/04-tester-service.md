# Tester un service

* Générer un nouveau projet Angular.

```
ng new angular-tests-par-la-pratique
```


## Tester une méthode

* Générer un service

```
ng g service compteur
```

Les fichiers suivants sont créés :

```
/src/app
    compteur.service.ts
    compteur.service.spec.ts
```

Un service est créé :

```ts
import { Injectable } from '@angular/core';

@Injectable()
export class CompteurService {

  constructor() { }

}
```

Le test associé aussi :

```ts
// TestBed est une classe utilitaire fournie par Angular.
// Elle permet de créer un module Angular spécifiquement pour les tests
// inject est une fonction permettant de bénéficier de 
// l'injection de dépendance dans le cadre de nos tests.
import { TestBed, inject } from '@angular/core/testing';

// La classe compteur
import { CompteurService } from './compteur.service';


// describe est une fonction du framework Jasmine
// Il définit un ensemble de cas de tests
describe('CompteurService', () => {

  // beforeEach est une fonction Jasmine exécutée avant chaque cas de test
  beforeEach(() => {
  
    // création d'un module Angular pour le test
    // ce module est composé d'un service CompteurService
    TestBed.configureTestingModule({
      providers: [CompteurService]
    });
  });

  // it est une fonction Jasmine
  // il représente un cas de test
  // inject() permet ici de récupérer une instance du service via l'injection de dépendance.
  it('should be created', inject([CompteurService], (service: CompteurService) => {
    
    // A ce stade, nous avons une instance de CompteurService via la variable service
  
    // expect et toBeTruthy() sont des assertions Jasmine
    // ici le test vérifie que le service est instancié
    expect(service).toBeTruthy();
  }));
});

```

* Lancer l'exécution des tests

```ts
ng test
```

* Compléter le service comme suit :

```ts
import { Injectable } from "@angular/core";

@Injectable()
export class CompteurService {
  private _nombre = 0;

  constructor() {}

  incrementer(): number {
    return 0;
  }
}
```

* Créer des cas de test pour la méthode `incrementer`.

```ts
it("le premier appel à incrementer() retourne 1", inject([CompteurService], (service: CompteurService) => {
    const resultat = service.incrementer();

      expect(resultat).toBe(1);
      
    })
);

it("deux appels à incrementer() retourne 2", inject([CompteurService], (service: CompteurService) => {
    service.incrementer();
    const resultat = service.incrementer();

      expect(resultat).toBe(2);
      
    })
);

```

* Vérifier que le test est KO. Compléter le service `CompteurService` pour rendre ces tests passant.

## Tester une méthode utilisant le client HTTP

* Générer un service

```
ng g service posts
```

Les fichiers suivants sont créés :

```
/src/app
    posts.service.ts
    posts.service.spec.ts
```

* Ajouter le module HTTP Client

```ts
import { BrowserModule } from "@angular/platform-browser";
import { NgModule } from "@angular/core";
import { HttpClientModule } from "@angular/common/http";

import { AppComponent } from "./app.component";

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, HttpClientModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

* Compléter le service `PostsService` comme suit :


```ts
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable()
export class PostsService {
  constructor(private _http: HttpClient) {}

  recupererTousLesPosts(): Observable<any> {
    return this._http.get("https://jsonplaceholder.typicode.com/posts");
  }
}
```

* Compléter le test associé :

```ts
import { TestBed, inject } from "@angular/core/testing";

// Angular fournit un support pour les tests du client HTTP 
// via le module : HttpClientTestingModule
// Toutes les requêtes sont mockées
// HttpTestingController permet de contrôler le mock généré par Angular 
import {
  HttpClientTestingModule,
  HttpTestingController
} from "@angular/common/http/testing";

import { PostsService } from "./posts.service";

describe("PostsService", () => {
  
  // variable locale du contrôleur du mock HTTP Angular
  let httpTestingController: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      // import du module HTTP Client Test
      imports: [HttpClientTestingModule],
      providers: [PostsService]
    });
    
    // récupération de l'instance du contrôleur du mock HTTP Angular
    httpTestingController = TestBed.get(HttpTestingController);
  });

  // ...

  it("recupererTousLesPosts() envoie une requête HTTP vers https://jsonplaceholder.typicode.com/posts",
    inject([PostsService], (service: PostsService) => {
    
      // invocation de la méthode recupererTousLesPosts()
      // vérification du corps de la réponse HTTP
      service.recupererTousLesPosts().subscribe(posts => {
        // le résultat contient exactement 2 posts
        expect(posts.length).toBe(2);

        // vérification des résultats des titres
        expect(posts[0]["title"]).toBe("Titre 1");
        expect(posts[1]["title"]).toBe("Titre 2");
      });

      // vérifie qu'un appel HTTP vers https://jsonplaceholder.typicode.com/posts
      // a été émis une seule fois
      const requete = httpTestingController.expectOne(
        "https://jsonplaceholder.typicode.com/posts"
      );

      // vérifie que la requête émise à la méthode GET
      expect(requete.request.method).toEqual("GET");

      // déclenchement de la réponse HTTP
      // les observateurs sont alors notifiés
      requete.flush([{ id: 1, title: "Titre 1" }, { id: 2, title: "Titre 2" }]);
    })
  );

  afterEach(() => {
    // vérifie qu'il n'y aucune requête HTTP non prévue déclenchée
    httpTestingController.verify();
  });
});
```

La documentation officielle : https://angular.io/guide/http#testing-http-requests.

