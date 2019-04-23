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

L'isolation par défaut utilise la méthode `bridge`

```
docker stop mon-api
docker rm mon-api

docker run -d -p 5000:5000 -v $PWD:/src --name mon-api atelier/first-container
curl http://localhost:5000
```

On peut aussi restreindre les URLs d'écoute du host

```
docker stop mon-api
docker rm mon-api

docker run -d -p 5000:127.0.0.1:5000 -v $PWD:/src --name mon-api atelier/first-container

curl http://localhost:5000
ss -tunapl
```

## Creation d'un nouveau réseau

Finalement on peut aussi faire du custom.

```
docker network list
```

On y voit le réseau `host` ainsi que le réseau `bridge`.
Nous allons créer le réseau `mon-api-network` puis lancer notre conteneur dans
ce réseau

```
docker stop mon-api
docker rm mon-api

docker network create --subnet 172.42.0.0/16 mon-api-network
docker run -d --net mon-api-network -v $PWD:/src --name mon-api atelier/first-container
docker inspect mon-api

curl http://172.42.0.2:5000
```
