# Atelier 7: Debug et résolutions de problèmes

Tout d'abord, les logs.

```
sudo journalctl -fu backend.service
```

Sinon, vous pouvez regarder les informations sur le container

```
docker ps
docker inspect mon-api
```

Pour aller plus loin, nous avons des outils tel que `dive` pour explorer des images de container

```
docker run --rm -it \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v $(which docker):/bin/docker \
    wagoodman/dive:latest \
    atelier/first-container
```
