# Dockerization d'une application statique Flask

## Création de l'image

```
docker buildx build -t flaskapp .
```

## Execution du container

```
docker run --name myawesome-flask-app -d -p 8085:8000 flaskapp
```

## Vérification de l'état du container

```
docker ps -a -f name=myawesome-flask-app
```

## Affichage des logs en mode streaming

```
docker logs myawesome-flask-app -f
```



