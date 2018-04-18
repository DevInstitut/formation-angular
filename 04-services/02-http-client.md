# Client HTTP

## Module @angular/common/http

Angular n'impose pas d'outil pour effectuer une requête HTTP.

Vous pouvez utiliser ceux du marché.

* Il propose tout de même un outil indépendant permettant d'effectuer des requêtes HTTP.
* Le principal avantage de cet outil est son support des tests dans un environnement Angular.

## Activation du module

Le module `@angular/common/http` permet d'échanger avec un serveur HTTP.

```ts
// app.module.ts:
// ...
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [
    BrowserModule,
    // import du module HTTP
    HttpClientModule
  ]
})
export class MonModule {}
```

## Injecter le service HTTP

```ts
import {HttpClient} from '@angular/common/http';

@Component({
// ...
})
export class MonComposant {

  // injection du service HTTP
  constructor(private _http:HttpClient) {
  }
}
```
## Méthode du service Http

Le service Http met à disposition les méthodes suivantes :

* `get`
* `post`
* `put`
* `delete`
* `patch`
* `head`
* `request`

Toutes ces méthodes renvoient un objet `Observable<T>` qu'il est possible de transformer en objet `Promise<T>` via la méthode `toPromise()`.

Dans cette partie, nous allons nous concentrer sur l'exploitation des promesses.
Nous reviendrons sur le type `Observable<T>` dans la section `RxJS`.

## Exemple de requête `get`

```ts

 // requête HTTP : GET https://jsonplaceholder.typicode.com/posts

 this._http.get("https://jsonplaceholder.typicode.com/posts")
      .toPromise()
      .then((data: any) => {
            // cas ok 
      }, (error:any) => {
            // cas erreur
      );
```

Par défaut, la promesse contient le corps de la réponse.

Pour avoir accès à l'intégralité de la réponse :

```ts
import { HttpClient, HttpResponse } from "@angular/common/http";

(...)

this._http
      .get("https://jsonplaceholder.typicode.com/posts", {
        observe: "response"
      })
      .toPromise()
      .then((response: HttpResponse<any>) => {
        // récupération de la réponse
        // response.status => statut de la réponse
        // response.body => corps de la réponse
      });
```

## Gérer les erreurs

Les erreurs peuvent être récupérées :

```ts
import { HttpClient, HttpResponse, HttpErrorResponse } from "@angular/common/http";

(...)

this._http
      .get("https://jsonplaceholder.typicode.com/posts", {
        observe: "response"
      })
      .toPromise()
      .then((response: HttpResponse<any>) => {
        // récupération de la réponse
        // response.status => statut de la réponse
        // response.body => corps de la réponse
      }, (error: HttpErrorResponse) => {
           console.log("error", error);
     });
```

ou avec un `catch`:

```ts
import { HttpClient, HttpResponse, HttpErrorResponse } from "@angular/common/http";

(...)

this._http
      .get("https://jsonplaceholder.typicode.com/posts", {
        observe: "response"
      })
      .toPromise()
      .then((response: HttpResponse<any>) => {
        // récupération de la réponse
        // response.status => statut de la réponse
        // response.body => corps de la réponse
      })
      .catch((error: HttpErrorResponse) => {
        // cas d'erreur
      });
```

## Récupérer autre chose que du JSON

```ts
this._http
  .get("https://jsonplaceholder.typicode.com/posts", {
    responseType: 'text'
  })
  .toPromise()
  .then((data:string) => {
  
   // data représente le texte du corps de la réponse
   
   });
```

## Envoyer des données au serveur


```ts
import {
  HttpHeaders
} from "@angular/common/http";

(...)

// Options de la requête HTTP
// ici le corps de la requête sera du JSON
const httpOptions = {
  headers: new HttpHeaders({
    "Content-Type": "application/json"
  })
};

// Envoie de la requête POST
this._http
  .post(
    // url d'accès au service
    "http://loisirs-web-backend.cleverapps.io/users",
    
    // corps de la réquête
    {
      name: "hello"
    },
    
    // options de la requête HTTP
    httpOptions
  )
  .toPromise()
  .then((data: any) => {
    console.log(data);
  })
  .catch((error: HttpErrorResponse) => {
    console.log("error", error);
  });

```