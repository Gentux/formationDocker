## Atelier Compose 2: network

Ici, on va juste observer ce qu'il se passe.

```
docker-compose -f docker-compose.yml -d up
docker network list
```

On va donc modifier le fichier `docker-compose.yml`

```
docker-compose -f docker-compose.yml -d up
docker network list
docker network inspect ateliercompose2_mon-api-compose-network
docker ps
docker inspect ateliercompose2_mon-api_1
```
