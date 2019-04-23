## Atelier 7 : Isolation Réseau

Depuis le début des ateliers, nous utilisons simplement la notion de «
`publish` »

Ceci fonctionne car par défaut, nous sommes sur une configuration en mode
`bridge` que docker à gérer pour nous.

Dans cette atelier, nous allons creuser cet aspect

## Pas d'isolation du tout

Il existe plusieurs driver pour le réseau, comme on a vu qu'un process dans un
container, c'est comme un vrai process mais dans une boite, on peut se passer
de l'isolation:

```
docker stop mon-api
docker rm mon-api

docker run -d --net host -v $PWD:/src --name mon-api atelier/first-container
curl http://localhost:5000
```

## Isolation par défaut
