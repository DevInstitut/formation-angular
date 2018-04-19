# Configuration du routeur

Le module `RouterModule` doit être intégré au module applicatif.

Exemple :

```ts
import { RouterModule, Routes } from '@angular/router';

const appRoutes: Routes = [

  { path: 'page1', component: AComponent }, // /page1 affiche le composant A
  
  { path: 'page2', component: BComponent }, // /page2 affiche le composant B
  
  { path: '',   redirectTo: '/page1', pathMatch: 'full' }, // redirige vers la route page1 par défaut
  
  { path: '**',  component: PageNonTrouveeComponent } // page non trouvée
];

@NgModule({
    ...,
    imports: [
        ...,
        RouterModule.forRoot(appRoutes)
    ],
    ...
})
export class AppModule { }
```

## RouterOulet

Exemple de fichier : `src/app/app.component.html`.

```html
<header>
     <!-- Entête -->
</header>
<nav>
    <!-- Navigation via un menu -->
</nav>
<div id="content">
    <!-- le composant défini dans la route courante va être inséré à cet endroit -->
    
    <!-- au regard de la configuration précédente, 
        /page1 va insérer le composant AComponent à cet emplacement
        /page2 a insérer le composant BComponent à cet emplacement
    -->
    <router-outlet></router-outlet>
</div>
<footer>
     <!-- Pied de page -->
</footer>
```
