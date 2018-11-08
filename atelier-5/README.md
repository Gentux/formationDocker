## Atelier 5 : On va maintenant utiliser un volume

On va modifier le Dockerfile pour activer le live reload sur notre application

On nettoie, on rebuild et on relance le container:
```
docker kill mon-api
docker rm mon-api
docker build \
  --build-arg http_proxy=$http_proxy \
  --build-arg no_proxy=$no_proxy \
  --tag atelier/first-container .

docker run -d -p 5000:5000 -v $PWD:/src --name mon-api atelier/first-container
docker logs -f mon-api
```

Et maintenant on peut tester le live reload
