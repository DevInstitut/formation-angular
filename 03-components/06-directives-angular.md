# Directives Angular

Les directives de structure sont des composants permettant d’utiliser des structures de contrôles (if, for, ...) dans un template.

Il s'agit de composants spécifiques n’ayant pas de template mais définissant un comportement.

Angular fournit plusieurs directives de structures : `ngIf`, `ngFor`, `ngSwitch`, ...

Les directives de structure Angular sont pré-chargées.

## ngIf

`ngIf` permet d’utiliser la structure conditionnelle **SI**.

Exemple :

```html
<div *ngIf="age > 18"><h2>Adulte</h2></div>
```

Le contenu n'est construit que si la condition est vraie.

Autres formes de `*ngIf`.

```html
<div *ngIf="condition; else elseBlock">...</div>
<ng-template #elseBlock>...</ng-template>
```

```html
<div *ngIf="condition; then thenBlock else elseBlock"></div>
<ng-template #thenBlock>...</ng-template>
<ng-template #elseBlock>...</ng-template>
```

```html
<div *ngIf="condition as value; else elseBlock">{{value}}</div>
<ng-template #elseBlock>...</ng-template>
```

## ngForOf

La directive `ngForOf` est particulièrement utile pour afficher une liste d'éléments.

Elle instancie un fragment de vue pour chaque élément d’une collection.

```ts
import {Component} from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: `
        <h1>Itération</h1>
        <ul>
            <li *ngFor="let obj of maListe">{{obj.nom}}</li>
        </ul>
    `
})
export class MonComposant {

    maListe:any[] = [
        {nom:'nom 1'},
        {nom:'nom 2'}
    ];
}
```

La directive `ngFor` met à disposition des variables implicites.
* `index` : l'index de l’itération peut être trouvé.
* `even` : un booléen qui sera vrai si l'élément a un index pair
* `odd` : un booléen qui sera vrai si l'élément a un index impair
* `last` : un booléen qui sera vrai si l'élément est le dernier de la collection.

## ngSwitch

La directive `ngSwitch` fournit la structure conditionnelle `switch` (différent du switch Java, seul un cas est exécuté).

Exemple :

```html
<div [ngSwitch]="nombreMessage">
    <p *ngSwitchWhen="0">Pas de message</p>
    <p *ngSwitchWhen="1">1 message</p>
    <p *ngSwitchDefault>Plusieurs messages</p>
</div>
```

## ngStyle
* Permet de modifier plusieurs styles en même temps.
* La clé peut-être en camelCase (fontWeight) ou en dash-case (font-weight).

```html
<div [ngStyle]="{fontWeight: fontWeight, color: color}">Style dynamique</div>
```

## ngClass

La directive `ngClass` permet d’ajouter ou d’enlever dynamiquement une classe.

```html
<div [class.maClasse]="activerMaClasse()">La Classe</div>

<!-- ou -->
<div [ngClass]="{'maClasse1': activerMaClasse1(), 'maClasse2': activerMaClasse2()}">La Classe</div>
```