## Atelier Compose 1

Docker compose est un wrappeur autour de docker.
Il permet de manager plusieurs conteneurs avec une seule commande

## Start: docker-compose.yml

Regardez en premier lieu le contenu du fichier `docker-compose.yml` qui décrit
notre installation

```
docker-compose up
```

On peut aussi spécifier explicitement le fichier a utiliser et utiliser
l'option `daemon` pour faire tourner tout ça en arrière plan

```
docker-compose -f docker-compose.yml -d up
```

Et ensuite vérifier le résultat:

```
docker ps
```

On peut éteindre le déploiement

```
docker-compose down
```
