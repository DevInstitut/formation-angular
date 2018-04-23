# Tester un composant simple

```
ng g component banniere
```

```
create src/app/banniere/banniere.component.css (0 bytes)
create src/app/banniere/banniere.component.html (27 bytes)
create src/app/banniere/banniere.component.spec.ts (642 bytes)
create src/app/banniere/banniere.component.ts (277 bytes)
update src/app/app.module.ts (458 bytes)
```

* Modifier le template :

```html
<h1>{{titre}}</h1>
```

* Modifier le composant :

```ts
import { Component, OnInit } from "@angular/core";

@Component({
  selector: "app-banniere",
  templateUrl: "./banniere.component.html",
  styleUrls: ["./banniere.component.css"]
})
export class BanniereComponent implements OnInit {
  titre: string;

  constructor() {}

  ngOnInit() {
    this.titre = "Super titre";
  }
}
```

* Exemple de test vérifiant le titre :

```ts
// TestBed : pour créer un module Angular plus léger pour les tests
// ComponentFixture : gérer le cycle de vie d'un composant Angular
// async : gérer une tâche asynchrone
import { async, ComponentFixture, TestBed } from "@angular/core/testing";

// La classe du composant à tester
import { BanniereComponent } from "./banniere.component";

describe("BanniereComponent", () => {
  // l'instance du composant
  let component: BanniereComponent;

  // instance permettant de débugger et tester un composant
  let fixture: ComponentFixture<BanniereComponent>;

  beforeEach(async(() => {
    // création du module de test
    TestBed.configureTestingModule({
      // inclusion du composant à tester
      declarations: [BanniereComponent]
    })
      // compilation des composants graphiques du module
      .compileComponents();
  }));

  beforeEach(() => {
    // récupération des instances
    fixture = TestBed.createComponent(BanniereComponent);
    component = fixture.componentInstance;

    // provoquer la détection du changement
    // cette action valorise les expressions Angular du template
    fixture.detectChanges();
  });

  it("should create", () => {
    expect(component).toBeTruthy();
  });

  it('le titre devrait être "Super Titre"', () => {
    // récupération du template
    const banEl: HTMLElement = fixture.nativeElement;

    // recherche du premier élément <h1></h1>
    const h1 = banEl.querySelector("h1");

    // vérification du titre
    expect(h1.textContent).toEqual("Super titre");
  });
  
  it("le titre est piloté par la propriété titre du composant", () => {
      // modification du titre
      component.titre = "Super titre 2";
  
      // réévaluation du template
      fixture.detectChanges();
  
      // récupération du template
      const banEl: HTMLElement = fixture.nativeElement;
  
      // recherche du premier élément <h1></h1>
      const h1 = banEl.querySelector("h1");
  
      // vérification du titre
      expect(h1.textContent).toEqual("Super titre 2");
   });
});
```

* Vérifier que tous les tests sont passants.
