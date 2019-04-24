## Atelier Compose 3: stockage partagé

Nous pouvons partagé des données entre container.
Regardons la sections `storages` du fichier `docker-compose.yml`

```
docker-compose up -d
docker ps
```

Nous allons maintenant ajouter un fichier dans le volume depuis le container
`mon-api` et voir ce fichier dans le container `redis`

```
docker exec --user root -it ateliercompose3_mon-api_1 touch /src/partage/fichierPartage
docker exec --user root -it ateliercompose3_redis_1 ls -l /opt
```
