## Atelier 8 : Persistence des données

On a pas mal utiliser les volumes pour rafraîchir le code dans le conteneur.
Nous allons aller un peu plus loin cette fois-ci pour l'aspect backup.

## Fonctionnement du volume

```
docker stop mon-api
docker rm mon-api

# Aucun point de montage
mount | grep overlay

docker run -p 5000:5000 -v $PWD:/src -d --name mon-api atelier/first-container

# Point de montage type `overlay`
mount | grep overlay
```

Étant donnée qu'il s'agit d'un point de montage, la communication du volume et
bidirectionnel

On peut créer un fichier sur la machine host et le voir dans le container

```
touch unfichierHost
docker exec -it mon-api ls /src/

rm unfichierHost
```

On peut créer un fichier dans le container et le voir sur le host

```
docker exec -it mon-api ls /src/unfichierContainer
ls

rm unfichierContainer
```

## Montage en read-only

Nous pouvons aussi protéger notre configuration en écriture

```
docker stop mon-api
docker rm mon-api

docker run -d -p 5000:5000 -v $PWD:/src:ro --name mon-api atelier/first-container
docker inspect mon-api | jq .[0].Mounts
docker exec -it mon-api touch /src/toto
```

## Les logs

Si on se réfere au [12 factor apps](https://12factor.net/fr/). Les logs doivent
sortir sur la sortie standard.

De cette maniére, les logs sont capturé via `docker logs <container>`.

Et de cette manière, lorsque notre container est gérer par `systemd`, les logs
seront adressé à syslog où dans des fichiers spécifié qui pouront ensuite être
envoyé dans les outils de supervision.
