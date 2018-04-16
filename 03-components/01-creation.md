# Créer un composant

Un composant est une classe annotée avec le décorateur `@Component`.

Exemple de composant :

```ts
// Fichier *.ts
import {Component} from '@angular/core';

@Component({
    selector: 'mon-composant',
    template: '<h1>Ceci est mon composant</h1>'
})
export class MonComposant {
}
```

Il s'agit d'un bloc d’interface graphique réutilisable.

Il est généralement associé à un template (morceau de code HTML).

Le paramètre `selector` désigne balise HTML déclenchant l’affichage du composant.

Le paramètre `template` : le fragment HTML. (Utiliser `templateUrl` pour externaliser le template dans un fichier html).

Exemple d'utilisation du composant

```html
<body>
    <mon-composant>Ceci s'affiche avant que mon composant soit pris en charge</mon-composant>
</body>
```
