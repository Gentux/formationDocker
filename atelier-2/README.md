## Atelier 2 : Un premier container

Construisons notre premier Dockerfile:

* L'instruction `FROM`
* L'instruction `ENV`
* L'instruction `RUN`

Ensuite on construit notre container

```
docker build --build-arg http_proxy=$http_proxy --build-arg no_proxy=$no_proxy .
```
