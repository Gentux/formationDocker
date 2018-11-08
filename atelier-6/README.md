# Docker Dev

## Atelier 1 : Hello World

```
docker --version
docker run hello-world
docker run python:3.2 python --version
```

## Atelier 2 : Un premier container

Notre premier Dockerfile

```
FROM python:latest

ENV http_proxy $http_proxy
ENV https_proxy $http_proxy
ENV no_proxy $no_proxy

RUN pip install flask
```

Ensuite on le fait construit

```
docker build --build-arg http_proxy=$http_proxy --build-arg no_proxy=$no_proxy .
```

## Atelier 3 : Utiliser notre premier container

Nommer le container en le rebuildant

```
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag gentux/first-container .
```

Lancer le container

```
docker run gentux/first-container
```

Executer quelque choses dans le container

```
docker run --interactive --tty gentux/first-container python
```
ou bien en mode réduit:
```
docker run -it gentux/first-container python
```

Et dans votre interpreteur vous pouvez donc utiliser le module qu'on a
installer via l'instruction RUN de notre Dockerfile

```
import flask
```

## Atelier 4 : Faire tourner l'API dans le container et y acceder

Premièrement, on va mettre une petite application qui fournit une API dans notre container.

```
docker run --detach --name mon-api gentux/first-container
```

Ensuite, vous pouvez voir votre container via `docker ps` ou consulter les logs via
```
docker logs mon-api
```

Par contre, mon api n'est pas disponnible:
```
curl http://localhost:5000/
# => curl: (7) Failed to connect to localhost port 5000: Connexion refusée

docker kill mon-api
docker rm mon-api
```

On va maintenant exporter le port réseau pour accéder à notre API

```
docker run --detach --publish 5000:5000 --name mon-api gentux/first-container
```

```
curl http://localhost:5000/
# => Hello World !
```

## Atelier 5 : On va maintenant utiliser un volume

On va modifier le Dockerfile pour activer le live reload sur notre application

On nettoie, on rebuild et on relance le container:
```
docker kill mon-api
docker rm mon-api
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag gentux/first-container .

docker run -d -p 5000:5000 -v $PWD:/src --name mon-api gentux/first-container
docker logs -f mon-api
```

Et maintenant on peut tester le live reload

## Atelier 6: Lancer un container avec SystemD
