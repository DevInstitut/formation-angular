# Tester un composant lié à un service

* Créer un composant `CompteurComponent`.
```
ng g component compteur
```

* Modifier le template :

```html
<p>le compteur est à {{nb}}</p>

<button (click)="incrementer()">++</button>
```

* Modifier le composant :

```ts
import { Component, OnInit } from "@angular/core";
import { CompteurService } from "../compteur.service";

@Component({
  selector: "app-compteur",
  templateUrl: "./compteur.component.html",
  styleUrls: ["./compteur.component.css"]
})
export class CompteurComponent implements OnInit {
  private nb = 0;

  constructor(private _compteurSrv: CompteurService) {}

  ngOnInit() {
    this.nb = this._compteurSrv.incrementer();
  }

  incrementer() {
    this.nb = this._compteurSrv.incrementer();
  }
}
```

* Exemple de test vérifiant l'appel de la méthode `this._compteurSrv.incrementer()` :

```ts
import { async, ComponentFixture, TestBed } from "@angular/core/testing";

import { CompteurComponent } from "./compteur.component";
import { CompteurService } from "../compteur.service";

describe("CompteurComponent", () => {
  let component: CompteurComponent;
  let fixture: ComponentFixture<CompteurComponent>;

  // Création d'un service "bouchon"
  // Ceci est un test unitaire
  // Il ne doit tester que le composant
  let compteurServiceStub = {
    
    // ici la méthode incrémenter renvoie
    // systématiquement la valeur 14
    incrementer: () => 14
  };

  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [CompteurComponent],
      providers: [{ provide: CompteurService, useValue: compteurServiceStub }]
    }).compileComponents();
  }));

  beforeEach(() => {
    fixture = TestBed.createComponent(CompteurComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it("should create", () => {
    expect(component).toBeTruthy();
  });

  it("à l'initialisation le composant affiche l'incrément initial (ici 14)", () => {
    // récupération du template
    const compteurEl: HTMLElement = fixture.nativeElement;

    // recherche du premier élément <p></p>
    const phrase = compteurEl.querySelector("p");

    // vérification du texte
    // le nombre 14 fourni par le service bouchon est bien affiché dans la vue
    expect(phrase.textContent).toEqual("le compteur est à 14");
  });
});
```

* Vérifier que tous les tests sont passants.


