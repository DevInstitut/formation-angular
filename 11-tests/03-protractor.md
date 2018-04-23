# Protractor

*Protractor* est un framework de test E2E.

Protractor est un *wrapper* autour de WebDriverJS.

Il permet une intégration naturelle avec AngularJS et Angular.

Il s'utilise avec Jasmine (Mocha possible).

## Installation et lancement

* Installer Protractor

```
npm install -g protractor
```
  
* Installation de selenium server (standalone) et du chromedriver

```
webdriver-manager update
```	
  
* Lancement du standalone selenium server (nécessite un JDK)

```
webdriver-manager start
```

* Lancement du test avec Protractor

```
protractor conf.js
```

## Exemple de configuration

```js
exports.config = {		
  seleniumAddress:'http://localhost:4444/wd/hub',
  
  multiCapabilities:[
  { 'browserName': 'chrome'},	
  { 'browserName': 'firefox'}],	
  
  baseUrl: 'http://localhost:8080',	
  
  specs:	
  [	
  'spec/*_spec.js'	
  ]
};	


```

## Exemple de test

```js
describe('angularjs.org homepage', function() {
    
    it('should greet the named user',	function() {		
        browser.get('http://www.angularjs.org');	
            
        element(by.model('yourName')).sendKeys('Julie');	

        var greeting = element(by.binding('yourName'));

        expect(greeting.getText()).toEqual('Hello	Julie!');
  });	
});
```

## API

* `browser` : wrapper autour de l’instance WebDriver. il permet de naviguer.
* `element` : permet d’interagir avec des élements
* `by` : permet de sélectionner des élements (par css, modèle , repeater...)

* API de Jasmine (expect...)

Documentation : http://www.protractortest.org/#/api