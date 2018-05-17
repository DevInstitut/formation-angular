# Variables locales

Angular va évaluer les expressions d'un template en recherchant la variable dans l'instance du composant et dans les variables locales.

Une variable est dite locale lorsqu'elle ne provient pas de la classe du composant.

Elle est locale au template.

```html
<input type="text" #saisie>
{{ saisie.value }}
<button (click)="saisie.focus()">Focus</button>
```

* La déclaration d'une variable locale se fait via `#<variable>`