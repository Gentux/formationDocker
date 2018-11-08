# Atelier 4 : Faire tourner l'API dans le container et y acceder

Premièrement, on va mettre une petite application qui fournit une API dans notre container.
Pour cela on doit modifier notre Dockerfile:

* L'instruction `WORKDIR`
* L'instruction `COPY`
* L'instruction `CMD`

```
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag atelier/first-container .
docker run --detach --name mon-api atelier/first-container
```

Ensuite, vous pouvez voir votre container via `docker ps` ou consulter les logs via

```
docker ps
docker logs mon-api
```

Par contre, mon api n'est pas disponnible:
```
curl http://localhost:5000/
# => curl: (7) Failed to connect to localhost port 5000: Connexion refusée
```

On va stoper et détruire ce container
```
docker kill mon-api
docker rm mon-api
```

On va maintenant exporter le port réseau pour accéder à notre API

```
docker run --detach --publish 5000:5000 --name mon-api atelier/first-container
```

```
curl http://localhost:5000/
# => Hello World !
```
