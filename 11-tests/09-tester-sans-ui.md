# Tester sans interface graphique

Il peut être intéressant de configurer les tests pour qu'ils s'exécutent avec un navigateur sans interface graphique.

Les avantages recherchés :

* les tests seront exécutés plus rapidement
* les tests sont compatibles avec un environnement d'intégration continue sans interface graphique.

Configurer le fichier `karma.conf.js` :

```js

// ...

// remplacer Chrome par ChromeHeadless
 browsers: ["ChromeHeadless"],
 
 
// ...

```

Nous utilisons ici `Chrome Headless`, une version de Chrome sans interface graphique.
Ce produit est aujourd'hui le principal concurrent à `PhantomJS` (précurseur sur le sujet).

* Exécuter les tests unitaires et les tests E2E.



