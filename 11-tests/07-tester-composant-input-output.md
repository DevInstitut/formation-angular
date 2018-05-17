# Tester un composant paramétrable

* Créer une classe `Personne`

```
ng g class personne
```

* Compléter la classe `Personne` comme suit :

```ts
export class Personne {
  constructor(public nom: string, public prenom: string) {}
}
```

* Créer un composant `ProfilComponent`

```
ng g component profil
```

* Modifier le template :

```html
<label>{{personne?.nom}} - {{personne?.prenom}}</label>
<button id="aimer" (click)="donnerAvis(true)">J'aime</button>
<button id="detester" (click)="donnerAvis(false)">Je déteste</button>
```

* Modifier le composant :

```ts
import { Component, OnInit, Input, Output, EventEmitter } from "@angular/core";
import { Personne } from "../personne";

@Component({
  selector: "app-profil",
  templateUrl: "./profil.component.html",
  styleUrls: ["./profil.component.css"]
})
export class ProfilComponent implements OnInit {
  @Input() personne: Personne;
  @Output() avis = new EventEmitter<boolean>();

  constructor() {}

  ngOnInit() {}

  donnerAvis(avis: boolean) {
    this.avis.emit(avis);
  }
}

```

* Exemples de test :

```ts
import { async, ComponentFixture, TestBed } from "@angular/core/testing";

import { ProfilComponent } from "./profil.component";
import { Personne } from "../personne";
import { By } from "@angular/platform-browser";

describe("ProfilComponent", () => {
  let component: ProfilComponent;
  let fixture: ComponentFixture<ProfilComponent>;

  beforeEach(async(() => {
    TestBed.configureTestingModule({
      declarations: [ProfilComponent]
    }).compileComponents();
  }));

  beforeEach(() => {
    fixture = TestBed.createComponent(ProfilComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it("should create", () => {
    expect(component).toBeTruthy();
  });

  // test avec valorisation de @Input()
  it("avec une personne ayant un nom et un prénom", () => {
    const p = new Personne("Hugues", "Paul");

    // valorisation de l'input
    component.personne = p;
    fixture.detectChanges();

    // récupération du template
    const hostEl: HTMLElement = fixture.nativeElement;

    // recherche du premier élément <label></label>
    const phrase = hostEl.querySelector("label");

    // vérification du libellé
    expect(phrase.textContent).toEqual("Hugues - Paul");
  });

   // test sur l'émission d'événement @Output()
  it("un clic sur J'aime émet true", () => {
  
    // abonnement à l'émetteur d'événement
    let avis = false;
    component.avis.subscribe(av => (avis = av));
    
    // simulation du click sur le bouton `aimer`
    const hostDe = fixture.debugElement;
    const btnDe = hostDe.query(By.css("button#aimer"));

    btnDe.triggerEventHandler("click", null);

   // vérification de l'avis
    expect(avis).toEqual(true);
  });
});

```

* Vérifier que tous les tests sont passants.


