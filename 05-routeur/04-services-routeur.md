# Services

Le routeur Angular met a disposition des services.

## ActivatedRoute

Dans un composant, il est possible de récupérer les informations de la route active (https://angular.io/guide/router#activated-route).

Supposons que le routeur soit configuré comme suit :

```ts
const routes: Routes = [
    { path: 'pizzas/:id', component: PageDetail },
     ...
];
```

`:id` designe ici que le chemin est variable. Exemples de chemin : `/pizzas/12`, `pizzas/130`.

Pour récupérer le paramètre `id` du chemin, utiliser le service `ActivatedRoute`.

```ts
import { ActivatedRoute } from '@angular/router';

export class PageDetail {

    id: string;

    // Injection du service ActivatedRoute
    constructor(private route: ActivatedRoute) {

        // récupération du paramètre id
        this.id = route.snapshot.paramMap.get("id")
    }
}
```

## Router

Le service `Router` donne la possibilité de naviguer dans l'application de manière programmatique.

```ts
import { Router } from '@angular/router';
// ...
export class PageDetail {

    // Injection du service Router
    constructor(private router: Router) {
    }

    changerDePage() {

        // Navigation vers une page
        this.router.navigate(['/page1'])
        // this.router.navigate(['/page2',  {id: 12 }])
    }
}
```
