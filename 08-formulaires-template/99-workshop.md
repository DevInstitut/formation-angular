# Top Collègues #6

## AjouterUnCollegueComponent

Créer le formulaire suivant en le **pilotant par le template**.

![](../images/AjouterCollegueComponent.png)

Les contraintes :
* Le pseudo doit avoir au moins 2 caractères.
* Seuls les champs `Matricule` et `Pseudo` sont obligatoires.
* Le bouton `Ajouter` n'est actif que si tous les champs sont valides. 

Le formulaire est accessible depuis :
* le chemin `/collegues/nouveau`
* un bouton *Ajouter un collegue* à insérer dans le composant `ListeColleguesComponent`

Gérer les erreurs du serveur.

Dans le cas où le collègue a bien été ajouté côté serveur, rediriger l'utilisateur vers l'accueil.

## Ajout d'un collègue côté serveur.

L'application `Top Collegues` n'a pas la responsabilité de créer un collègue dans notre système d'information.

Les informations gérées par `Top Collegues` sont : le pseudo, le score, les votes.

Elle n'a, par exemple, pas le droit de modifier le nom du collègue.

L'idée serait que le client envoie les informations suivantes :

```
{
    "matricule" : "XXX",
    "pseudo": "XXX",
    "urlImage" : "XXX"
}
```

Le serveur, à partir du `matricule`, fait sur recherche de ce matricule sur une application dédiée via une requête HTTP.

Si le collègue est trouvé, alors il est inséré dans la base de données de `Top Collègues`.


### API Collegues

* Trouver la liste des collègues : http://collegues-api.cleverapps.io/collegues


* Rechercher un collègue à partir du matricule : http://collegues-api.cleverapps.io/collegues?matricule=75e8048c





 