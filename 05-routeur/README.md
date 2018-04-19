# Routeur

Un routeur permet d'établir une navigation basée sur les URL de l'application.

Dans une _Single Page Application_, il y a deux options :

* mode **hashbang**.

* mode **HTML 5**.

## Mode _hashbang_

Les chemins utilisent les ancres HTML (caractère _#_).

```
http://www.monsite.fr/#page1
http://www.monsite.fr/#page2
```

## Mode _HTML 5_

Les chemins sont _classiques_ (sans _#_) :

```
http://www.monsite.fr/page1
http://www.monsite.fr/page2
```

Cela est possible par le fait que le navigateur autorise la création d'une nouvelle entrée dans son historique sans effectuer de requête vers le serveur.

```js
var stateObj = { foo: "bar" }; // donnée associée à l'état
history.pushState(stateObj, "page 2", "bar.html"); // alimenter l'historique
```

Pour en savoir plus : https://developer.mozilla.org/fr/docs/Web/Guide/DOM/Manipuler_historique_du_navigateur.