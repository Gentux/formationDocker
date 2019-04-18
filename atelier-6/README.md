## Atelier 6 : Aspect process du container

La bonne pratique pour les container, c'est de faire 1 process égal 1
container.

Et dans cette optique, quand une équipe de dev me demande 8Go de RAM pour son
projet, moi j'exige de pouvoir faire tourner 8 process de 1Go de RAM chacun

On peut utiliser les conteneur pour vérifier ça

## Limiter la mémoire ou le CPU

Malheureusement, pour faire cette partie, il faudra un kernel `real-time` qui
n'est pas installé par défaut.

On nettoie, on rebuild et on relance le container:
```
docker stop mon-api
docker kill mon-api
docker rm mon-api

docker run -d -p 5000:5000 -v $PWD:/src --name mon-api --memory=500m atelier/first-container
docker inspect mon-api
```

## Les process dans un container ou en dehors

Essayons de lister les processus dans le container

```
sudo ps aux | grep python
docker exec -it mon-api ps -aux
```

Pas besoin de grep dans le container, le container ne « voit » que ce qu'il y a
dans le container

On peut aussi observer que les PID ne sont pas les mêmes

Et on peut aussi voir que l'utilisateur `root` dans le container est aussi
l'utilisateur `root` sur la machine. Ici on a un problème de sécurité.

```
docker stop mon-api
docker rm mon-api
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag atelier/first-container .

docker run -d -p 5000:5000 -v $PWD:/src --name mon-api atelier/first-container
sudo ps aux | grep flask
```
