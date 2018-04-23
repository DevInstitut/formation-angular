# Jasmine

![center](images/jasmine.png)

Un **framework de test JavaScript**.

Orienté BDD (Behavior-Driven Development – **Développement piloté par le comportement**).

> Ecriture de tests que *tout le monde peut comprendre*.

# Jasmine - Exemple de test

```js
 it("12 + 5 doit être égal à 17", () => {
    var a = 12;
    var b = 5;
    var resultat = a + b; 

    expect(resultat).toBeDefined();
    expect(resultat).toBe(17);
    expect(resultat).not.toBe(a);  
 });
```


# Jasmine - Exemple de suite de tests

```js
describe("Une suite avec 2 tests", () => {

 it("12 + 5 doit être égal à 17", () => {
    var a = 12;
    var b = 5;
    var resultat = a + b; 
    expect(resultat).toBeDefined();
    expect(resultat).toBe(17);
    expect(resultat).not.toBe(a);  
 });

 it("L'égalité de deux objets est bien gérée", () => {
    var a = { prop1 :"val1", prop2 : "val2" };
    var b = { prop1 :"val1", prop2 : "val2" };
    expect(a).toEqual(b); 
 });
}
```

# Jasmine - Fixture

Jasmine supporte plusieurs fixtures :

* `beforeAll`
* `beforeEach`
* `afterAll`
* `afterEach`


Exemple de Fixtures :

```js
describe("Une suite avec 2 tests", () => {
 beforeEach(() => {
    this.valeur = 5;
 });
 afterEach(() => {
    this.count = 1;
 });
 it("test 1", () => {
    expect(this.valeur).toEqual(5); 
    expect(this.count).not.toBeDefined();
 });
 it("test 2", () => {
     expect(this.count).toBeDefined(); 
 });
}
```


# Jasmine - Suite imbriquée

```js
describe("Une suite", () => {
   it("test 1", () => {
      // code du test
   });

   describe("Une suite imbriquée", () => {

     it("test suite imbriquée 1", () => {
        // code du test
     });

     it("test suite imbriquée 2", () => {
        // code du test
     });
   }
}
```