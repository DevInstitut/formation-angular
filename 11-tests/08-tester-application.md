# Tester l'application (E2E)

Angular CLI intègre par défaut [Protractor](https://www.protractortest.org/#/) comme framework de test navigateur.

Les tests E2E sont dans le répertoire `e2e` :

```ts
/e2e
    /src
        app.e2e-spec.ts
        app.po.ts
    tsconfig.e2e.json
```

Le fichier `app.po.ts` contient une classe de structure de la page principale :

```ts
// outillage protractor
// browser => manipulation du navigateur (changer de page, rafraichir la page, ...)
// by => utilitaire pour cibler des éléments du DOM
// element => manipulation d'un élément du DOM
import { browser, by, element } from 'protractor';

export class AppPage {

  // méthode utilitaire pour aller à la page racine
  navigateTo() {
    return browser.get('/');
  }

  // récupération du texte du paragraphe
  getParagraphText() {
    return element(by.css('app-root h1')).getText();
  }
}
```

API de protractor : https://www.protractortest.org/#/api.

* Compléter le fichier `app.component.html` pour y ajouter le composant `<app-compteur></app-compteur>`.

Nous allons à présent créer un test navigateur qui simule l'utilisation du compteur.

* Créer une structure qui permet de récupérer les différentes parties de ce composant : le bouton et le paragraphe (fichier `e2e/compteur/compteur.po.ts`).

```ts
import { browser, by, element } from "protractor";

export class CompteurCmp {
  getBtnIncrementer() {
    return element(by.css("app-compteur button"));
  }

  getParagraph() {
    return element(by.css("app-compteur p"));
  }
}
```

* Compléter la page `AppPage` pour rendre accessible le composant `CompteurCmp` :


```ts
import { browser, by, element } from "protractor";
import { CompteurCmp } from "./compteur/compteur.po";

export class AppPage {
  compteurCmp = new CompteurCmp();
  navigateTo() {
    return browser.get("/");
  }

  getParagraphText() {
    return element(by.css("app-root h1")).getText();
  }
}

```

* Ecrirer un test E2E `e2e/src/compteur/compteur.e2e-spec.ts` :

```ts
import { AppPage } from "../app.po";

describe("angular-tests-par-la-pratique App", () => {
  let page: AppPage;

  beforeEach(() => {
    page = new AppPage();
  });

  it("au lancement le compteur est à 1", () => {
    page.navigateTo();
    expect(page.compteurCmp.getParagraph().getText()).toEqual(
      "le compteur est à 1"
    );
  });

  it("après 2 clicks le compteur est à 3", () => {
    page.navigateTo();
    page.compteurCmp.getBtnIncrementer().click();
    page.compteurCmp.getBtnIncrementer().click();
    expect(page.compteurCmp.getParagraph().getText()).toEqual(
      "le compteur est à 3"
    );
  });
});
```

* Lancer le test E2E

```
ng e2e
```

> Attention : il faut que l'application soit démarrée (`ng serve`) pour que les tests puissent passer.