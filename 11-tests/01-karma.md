# Karma

Karma est **un exécuteur de test JavaScript** basé sur Node.js et distribué en tant que package Node.

Il intègre de nombreux environnements d'exécution : 

* Chrome, Chrome Canary, 
* Internet Explorer (Windows uniquement), 
* Firefox, 
* Safari (Mac uniquement),  
* PhantomJS, Opéra, etc.

## Karma
Il supporte **plusieurs frameworks de tests unitaires** : 

* Jasmine
* QUnit
* Mocha

Il est possible d'étendre ce support via l'écriture d'adaptateur.

Karma s'utilise en ligne de commande ou via une intégration dans d'autres outils (JetBrains WebStorm IDE, Grunt, Gulp, etc.)

## Karma - Mise en oeuvre

Installation

```bash
npm install -g karma-cli

npm install karma karma-jasmine karma-chrome-launcher
```
Générer un fichier de configuration Karma

```
karma init <nom_fichier_config.js>
```

Lancer Karma

```
karma start <nom_fichier_config.js>
```