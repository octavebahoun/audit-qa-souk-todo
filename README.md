# audit-qa-souk-todo

Dépôt public de test, inoffensif, créé pour l’audit QA fonctionnel de [Souk.dev](https://soukdev.shop). Préfixe `audit-` convenu avec le propriétaire du compte. Il ne contient aucun secret et ne doit pas servir en production.

## Appli

Petite liste de tâches statique, servie par `nginx:alpine` sur le port 80. Tout se passe dans le navigateur : aucune base, aucune API, aucune donnée personnelle.

Fichiers à la racine :

- `index.html` — interface de la liste de tâches
- `Dockerfile` — image basée sur `nginx:alpine`
- `docker-compose.yml` — service `web`, port conteneur 80
- `soukdev.json` — manifeste Souk.dev (version 1, `backend: propre`, sans variables)

Lancer en local :

```bash
docker compose up --build
```

Puis ouvrir `http://localhost` si le port 80 de l’hôte est publié, ou interroger le port 80 du conteneur.

## Bug volontaire

Le bouton **Ajouter** accepte une tâche vide : une chaîne vide, ou seulement des espaces, est ajoutée à la liste. Aucune vérification ni message d’erreur n’est affiché.

Ce comportement est intentionnel. Il servira au parcours Souk.dev « signaler un bug, puis proposer un correctif » (refuser les tâches vides après `trim()`, et afficher un message clair).

## Manifeste `soukdev.json`

Le format suit le schéma officiel `soukdev.schema.json` (champs requis : `version`, `service_web`, `backend`, `variables`) et les fichiers publics déjà publiés, par exemple `octavebahoun/octavebahoun-houtoukpe` et `octavebahoun/marchilearnia`.
