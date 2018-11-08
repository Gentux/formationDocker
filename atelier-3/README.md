# Atelier 3 : Utiliser notre premier container

Mettre un tag sur notre container en le construisant à nouveau

```
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag atelier/first-container .
```

Lancer le container

```
docker run atelier/first-container
```

Executer quelque choses dans le container

```
docker run --interactive --tty atelier/first-container python
```

Et dans votre interpreteur vous pouvez donc utiliser le module qu'on a
installer via l'instruction RUN de notre Dockerfile

```
import flask
```
