# Propriétés

## Propriétés DOM

Soit le code HTML suivant :

```html
<input type="text" value="bonjour">
```

Le navigateur créera un objet de type `HTMLInputElement` avec les champs :

* `type="text"`
* `value="bonjour"`

Le type `HTMLInputElement` contient beaucoup d'autres propriétés : https://developer.mozilla.org/fr/docs/Web/API/HTMLInputElement.

## Propriétés DOM & interpolation Angular

Soit le code suivant :

```html
<input type="text" value="{{exp}}">
```

Le navigateur créera un objet de type `HTMLInputElement` avec les champs :

* `type="text"`
* `value="valeur obtenue à partir de l'expression"` : Angular aura évalué l'expression et mis à jour la propriété `value`.

Les objets du navigateur ayant un grand nombre de propriétés pas toujours accessible via les attributs HTML,
Angular met à disposition un mécanisme permettant de valoriser une propriété d'un objet du DOM.

L'exemple précédent peut s'écrire :

```html
<input type="text" [value]="exp">
```

Prenons un autre exemple.

Soit le code suivant :

```
<p>{{unObjet.prop}}</p>
```

Cette notation est un raccourci de :

```
<p [textContent]="unObjet.prop"><p/>
```

## Binding de propriété

Angular permet d'intervenir directement sur les propriétés des objets du DOM.

Cela offre une grande flexibilité sur les options possibles. Angular n'est plus obligé de fournir une liste finie d'attributs.

Quelques exemples :

```html

<mon-cmp [name]="user.name"></mon-cmp>

<div [hidden]="estCache">Est Caché ?</div>

<p [style.color]="maCouleur">Super ta couleur</p>

<p [textContent]="'Attention ceci est statique' + user.name"></p>

```

