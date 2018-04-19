# Pipes

Un pipe (tuyau) est un transformateur de données.
* Il permet de transformer des données brutes en une forme souhaitée.
* Angular fournit plusieurs types de pipe : `json`, `slice`, `uppercase`, `lowercase`, `number`, `percent`, `currency`, `date`, `async`.
* Il est possible de créer ses propres pipes.

Syntaxe :

```html

{{ VARIABLE | NOMPIPE }}
```

Exemple : 

```html

{{ monObject | async }}

```