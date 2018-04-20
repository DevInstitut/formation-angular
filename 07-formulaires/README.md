# Formulaires

Angular simplifie la gestion des formulaires (module `@angular/forms`).

2 stratégies :

* Formulaire piloté par le modèle (Reactive Forms)
 * module `ReactiveFormsModule`
 * chaque objet graphique est représenté par un objet JavaScript.
 * le pilotage est assuré en manipulant des objets JavaScript.
 * gestion `synchrone` du formulaire
* Formulaire piloté par le template (binding bi-directionnel)
 * module `FormsModule`
 * gestion `asynchrone` du formulaire


Quelque soit la stratégie, Angular ajoute et enlève automatiquement certaines classes CSS sur chaque champ de formulaire en fonction de son état.

Cela permet d'affiner le visuel du formulaire en fonction de son état.

* Ces classes sont :
 * `ng-valid`
 * `ng-invalid`
 * `ng-dirty`
 * `ng-pristine`
 * `ng-touched`
 * `ng-untouched`,
 * ...
