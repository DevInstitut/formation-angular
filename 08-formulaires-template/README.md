# Formulaire piloté par le template

* Similaire aux formulaires Angular 1.x.

* La configuration est plutôt portée par le template et moins par la classe du composant.

```ts
// ...
import { FormsModule }   from '@angular/forms';

@NgModule({
  imports: [//...,
    FormsModule // <--
  ],
  // ...
})
export class AppModule { }
```

## Binding bi-directionnel
Le binding bi-directionnel s'active avec la directive ngModel via la syntaxe `[(ngModel)]="exp"`.

```ts
class MonModel { val1:string; val2:string;}

@Component({
    selector: 'mon-form',
    template: `
        <h1>{{monModel.val1}}</h1>
        <form (ngSubmit)="submit()">

            <label>Champ 1</label><input [(ngModel)]="monModel.val1">

            <label>Champ 2</label><input [(ngModel)]="monModel.val2">

            <button type="submit">Submit</button>
        </form>`
})
export class MonForm {

    // la propriété monModel est mise à jour automatiquement avec la saisie utilisateur
    // grâce au binding bi-directionnel  [(ngModel)]
    monModel:MonModel = new MonModel();

    submit() {
        console.log(this.monModel);
    }
}
```

## Validation

Pour un formulaire piloté par le template, Angular fournit des directives à appliquer aux éléments du templates (required, minlength, ...)

Exemple :

```html
<form (ngSubmit)="submit(monForm.value)" #monForm="ngForm">
    <label>Champ 1</label>
    <input [(ngModel)]="monModel.val1" #champ1="ngModel" required minlength="3">

    <label>Champ 2</label>
    <input [(ngModel)]="monModel.val2" #champ2="ngModel" required>

    <button type="submit">Submit</button>
</form>
```

Les variables locales `champ1`, `champ2`, `monForm` sont des contrôles de formulaires qui contiennent plusieurs attributs (https://angular.io/api/forms/AbstractControl) :

* `valid` : si le champ est valide (contraintes & validations respectées).
* `errors` : objet contenant les erreurs du champ.
* `dirty` : vaut false jusqu'à ce que l'utilisateur modifie la valeur du champ.
* `pristine` : opposé de dirty.
* `touched` : false jusqu'à ce que l'utilisateur soit entré dans le champ.
* `untouched` : opposé de touched.
* `value` : la valeur du champ.
* `status` : VALID ou INVALID



