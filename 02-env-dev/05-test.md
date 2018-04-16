# ng test

La commande `ng test` permet d'exécuter les tests unitaires de l'application.

Exemple :

```
ng test
 10% building modules 1/1 modules 0 active15 04 2018 11:15:06.330:WARN [karma]: No captured browser, open http://localhost:9876/
15 04 2018 11:15:06.334:INFO [karma]: Front-end scripts not present. Compiling...                                                                                  15 04 2018 11:15:09.797:WARN [karma]: No captured browser, open http://localhost:9876/
15 04 2018 11:15:09.981:INFO [karma]: Karma v2.0.0 server started at http://0.0.0.0:9876/
15 04 2018 11:15:09.981:INFO [launcher]: Launching browser Chrome with unlimited concurrency
15 04 2018 11:15:09.985:INFO [launcher]: Starting browser Chrome
15 04 2018 11:15:10.967:INFO [Chrome 65.0.3325 (Linux 0.0.0)]: Connected on socket Ex0FVxGiYuPPhn6OAAAA with id 30960733
Chrome 65.0.3325 (Linux 0.0.0): Executed 3 of 3 SUCCESS (0.165 secs / 0.159 secs)
```

Par défaut, les tests tournent en continue.

`CTRL+C` pour arrêter l'exécution des tests.

Documentation officielle : https://github.com/angular/angular-cli/wiki/test.