# Dockerization d'une application statique PHP

## Création de l'image

```
docker buildx build -t phpapp .
```

## Execution du container

```
docker run --name myawesome-php-app -d -p 8086:8000 phpapp
```
Accéder au browser et vérifier: http://0.0.0.0:8086/ 

## Vérification de l'état du container

```
docker ps -a -f name=myawesome-php-app
```

## Affichage des logs en mode streaming

```
docker logs myawesome-php-app -f
```



