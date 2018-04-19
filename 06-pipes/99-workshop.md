# Top Collègues #5

## Pseudo en majuscule

* Utiliser un pipe Angular pour mettre tous les pseudos en majuscule.


## _Pipe_ `score`

* Générer un _Pipe_ personnalisé

```
ng g pipe pipes/Score
```

* Ce pipe sera appliqué aux scores de l'application.

```html
{{ scoreVal | score }}
```


* Ce pipe permet de formater un score :
 * taille de la police plus grande
 * code couleur différent suivant que le score est positif, négatif ou égal à 0.
 * le signe est toujours présent : `+ 120`, `- 50`.

## Filtre par pseudo

* Implémenter la possibilité de pouvoir filtrer par pseudo.

![](../images/ListeColleguesComponent2.png)