# Top Collègues #3

## Application Backend

* Créer une application Spring Boot _top-collegues-backend_.

```
spring init --dependencies=web,data-jpa,devtools,h2 top-collegues-backend
```

* Exposer le service _GET /collegues_ qui récupère la liste des collègues au format JSON. Voici un exemple de réponse :

```json
[
    {
      "score": 100,
      "pseudo": "Rod",
      "imageUrl": "https://images.pexels.com/photos/265036/pexels-photo-265036.jpeg?w=1260&h=750&auto=compress&cs=tinysrgb"
    },
    {
      "score": 800,
      "pseudo": "Alice",
      "imageUrl": "https://images.pexels.com/photos/265036/pexels-photo-265036.jpeg?w=1260&h=750&auto=compress&cs=tinysrgb"
    }
]
```

* Exposer un service _PATCH /collegues/PSEUDO/_ qui permet de mettre à jour le score d'un collègue.

Le corps de la réquête sera de la forme :

```json
{ "action" : "AIMER" }

// ou

{ "action" : "DETESTER"}

```
Ce service retourne l'objet Collegue à jour.
L'action `AIMER` incrémente le score de 10 points.

L'action `DETESTER` décrémente le scode de 5 points.

* Déployer l'application sur Heroku :
 * Via `maven-dependency-plugin` : https://devcenter.heroku.com/articles/java-webapp-runner.
 * Via `heroku-maven-plugin` : https://devcenter.heroku.com/articles/deploying-java-applications-with-the-heroku-maven-plugin.


## Front - Gérer les URLs backend

Notre application front va communiquer avec l'application back pour récupérer les données.

Il va falloir gérer 2 urls backend :
* `http://localhost:port` en mode développement
* `http://adresseheroku` en mode production

Vous pouvez pour cela utiliser le module environment `src/environments/environment`.

Vous configurez le fichier `src/environments/environment.ts` pour le mode développement. Exemple :

```ts

export const environment = {
  production: false,
  
  // ajout d'une URL backend en mode développement
  backendUrl: 'http://localhost:port'
};


```

Vous configurez le fichier `src/environments/environment.prod.ts` pour le mode production. Exemple :

```ts

export const environment = {
  production: false,
  
  // ajout d'une URL backend en mode développement
  backendUrl: 'http://adresseheroku'
};


```

A l'utilisation, :

```ts
import {environment} from '../environments/environment';


// en développement, URL_BACKEND = 'http://localhost:port'
// en mode production, URL_BACKEND = 'http://adresseheroku'
const URL_BACKEND = environment.backendUrl;


```




## Front - Service `CollegueService`

* Générer un service _Collegue_.

```
ng g service services/Collegue
```

* Compléter le service collègue pour consommer les services backend :

```ts
@Injectable()
export class CollegueService {

  constructor() { }

  listerCollegues():Promise<Collegue[]>  {
    // récupérer la liste des collègues côté serveur
  }

  donnerUnAvis(unCollegue:Collegue, avis:Avis):Promise<Collegue>  {
    // TODO Aimer ou Détester un collègue côté serveur
  }

}
```

A ce stade :
* les données sont désormais récupérées d'une application backend.
* les actions `AIMER` ou `DETESTER` mettent à jour la base de données.
* aucune mise à jour n'est faite sur le composant `HistoriqueVotesComponent`.
