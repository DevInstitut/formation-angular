# date

* Transforme une date en chaîne de caractères au format désiré.
Cette date peut être un objet Date ou un nombre en millisecondes

```html
 
  <p>{{ dateNaissance | date:'ddMMyyyy' }}</p> <!-- affiche '07/16/1986' -->
  
  <p>{{ dateNaissance | date:'longDate' }}</p> <!-- affiche 'July 16, 1986' -->
  
  <p>{{ dateNaissance | date:'HHmmss' }}</p>   <!-- affiche '15:30:00' -->

  <p>{{ dateNaissance | date:'shortTime' }}</p>  <!-- affiche '3:30 PM' -->
 
```