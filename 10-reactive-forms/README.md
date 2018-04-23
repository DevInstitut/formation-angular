# Formulaire piloté par le modèle


Principe :
* Construction de formulaire programmatiquement.
* Les champs du formulaire (input, select,...) sont représenté par un `Control` (objet javascript).

## Module `ReactiveFormsModule`

```ts
// ...
import { ReactiveFormsModule } from '@angular/forms';  // <--

@NgModule({
  imports: [//..
    ReactiveFormsModule // intégration du module ReactiveForms
  ], // ...
})
export class AppModule { }
```


## Création d'un contrôle.


```ts
import { FormControl } from '@angular/forms';

@Component({
  selector: "mon-cmp",
  template: `
  <label>Saisie :
    <input [formControl]="saisie">
  </label>
    `
})
export class MonComposant {
  saisie = new FormControl();
}
```

## Classes de base

* `AbstractControl` : classe abstraite de base des classes `FormControl`, `FormGroup`, `FormArray`.
* `FormControl` : suit la valeur et la validité d'un composant graphique de formulaire.
* `FormGroup` : gère un groupe d'instances de type `AbstractConrol`.
* `FormArray` : suit la valeur et la validité d'un tableau d'instances de type *AbstractConrol*.


`FormGroup` permet d'enregistrer plusieurs instances de `FormControl`.

```ts
import { FormControl, FormGroup } from '@angular/forms';

@Component({
  selector: "mon-cmp",
  template: `
  <form [formGroup]="monForm" novalidate>
      <label>Saisie : <input formControlName="saisie"></label>
  </form>
    `
})
export class MonComposant {
  monForm = new FormGroup ({ saisie: new FormControl() });
}
```

## `FormBuilder`
La classe `FormBuilder` simplifie la création des objets `Control`.

```ts
import { FormBuilder, FormGroup } from '@angular/forms';
// ...
export class MonComposant {
  monForm: FormGroup; // <---

  constructor(private fb: FormBuilder) { // <---
    this.monForm = this.fb.group({
          saisie1: '', // raccourci de  saisie1: this.fb.control('')
        });
  }
}
```

## Classe `Validators`

La classe `Validators` permet d'ajouter des règles de validation.

```ts
// ...
export class MonComposant {
  monForm: FormGroup;
  constructor(private fb: FormBuilder) {
    this.monForm = this.fb.group({
          saisie1: ['', Validators.required ], // ajout d'une règle de validation
          saisie2: '',
          saisie3: ''
        });
  }
}
```

Elle fournit plusieurs contraintes ::
Validators.required, Validators.minLength(...), ...

Elle permet de combiner plusieurs validateurs via sa méthode Validators.compose([...]).

```ts
this.champ1 = fb.control('',
    Validators.compose([
        Validators.required,
        Validators.minLength(3)
    ]);
this.champ2 = fb.control('', Validators.required);
```

## Attributs d'un contrôle

Un `Control` a plusieurs attributs (https://angular.io/api/forms/AbstractControl) ::
* `valid` : si le champ est valide (contraintes & validations respectées).
* `errors` : objet contenant les erreurs du champ.
* `dirty` : vaut false jusqu'à ce que l'utilisateur modifie la valeur du champ.
* `pristine` : opposé de dirty.
* `touched` : false jusqu'à ce que l'utilisateur soit entré dans le champ.
* `untouched` : opposé de touched.
* `value` : la valeur du champ.
* `status` : VALID ou INVALID
* `valueChanges` : un Observable qui émet un événement à chaque changement sur
le champ.
* `statusChanges` : un Observable qui émet un événement à chaque fois que le statut de la validation est recalculé.
* ...
...

## Méthode `get()`

La méthode `get()` d'un `FormControl` permet de récupérer un contrôle du groupe.

```html
<p>Saisie : {{ monForm.get('saisie').value }}</p>
```

## Mettre à jour le modèle

En créant un formulaire réactif, le modèle de données (venant du serveur) est distingué du modèle du formulaire (FormControl).

Pour mettre à jour le modèle du formulaire, utiliser les méthodes `setValue` ou `patchValue`.

```ts
// setValue => mise à jour complète
this.monForm.setValue({
  saisie1: this.modelServer.prop1,
  saisie2: this.modelServer.prop2
});
```

Pour une mise à jour différentielle, utiliser `patchValue`.

```ts
this.monForm.patchValue({
  saisie2: this.modelServer.prop2
});
```
