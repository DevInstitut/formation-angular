# ng build

La commande `ng build` compile l'application dans un répertoire de sortie (par défaut `dist`).

Documentation officielle : https://github.com/angular/angular-cli/wiki/build.

```
ng build
Date: 2018-04-15T09:31:25.700Z
Hash: f4ce2ce64bfb6b37cacb
Time: 8041ms
chunk {inline} inline.bundle.js, inline.bundle.js.map (inline) 3.89 kB [entry] [rendered]
chunk {main} main.bundle.js, main.bundle.js.map (main) 7.39 kB [initial] [rendered]
chunk {polyfills} polyfills.bundle.js, polyfills.bundle.js.map (polyfills) 204 kB [initial] [rendered]
chunk {styles} styles.bundle.js, styles.bundle.js.map (styles) 14.5 kB [initial] [rendered]
chunk {vendor} vendor.bundle.js, vendor.bundle.js.map (vendor) 2.44 MB [initial] [rendered]
```

Exemple de répertoire de sortie :

```
/ma-super-app
    /dist
        favicon.ico
        index.html
        inline.bundle.js
        inline.bundle.js.map
        main.bundle.js
        main.bundle.js.map
        polyfills.bundle.js
        polyfills.bundle.js.map
        styles.bundle.js
        styles.bundle.js.map
        vendor.bundle.js
        vendor.bundle.js.map
```





