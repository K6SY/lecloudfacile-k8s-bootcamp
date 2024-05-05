# Prise en main des commandes Docker

## Gestion des containers

- Création d'un nouveau container à partir d'une image

```
docker run <image-name>:<tag>
```

- Assignation d'un nom au container

```
docker run --name <nick-name> <image-name> 

```

- Execution en mode interactive

```
docker run -it <image-name>
```

- Execution en background

```
docker run -d <image-name>
```

- Exposition container sur le réseau de l'hôte

```
docker run -p <host-port>:<container-port> <image-name>
```

- Liste des containers en cours d'execution
```
docker ps
```

- Liste de l'ensemble des containers

```
docker ps -a
```

- Arrêt d'un ou plusieurs containers en cours d'execution

```
docker stop <IdContainer>
```

- Démarrage d'un ou de plusieurs containers à l'arrêt
```
docker start <IdContainer>
```

- Récupération des journaux (logs) d'un container

```
docker logs <IdContainer ou NomContainer>
```

- Récupération des journaux (logs) d'un container en mode stream

```
docker logs -f <IdContainer ou NomContainer>
```

- Execution d'une commande en mode interactive dans un conteneur en execution
```
docker exec -it <IdContainer ou NomContainer> <cmd>
```

- Copie de fichiers ou répertoire depuis le conteneur vers le système de fichier local

```
docker cp <IdContainer ou NomContainer>:</path/file.ext> .
```

- Copie de fichiers ou répertoire depuis le système de fichier local vers le conteneur 

``` 
docker cp <fichier ou repertoire> <IdContainer ou NomContainer>:</path/>
```

- Suppression d'un conteneur à l'arrêt

```
docker rm <IdContainer ou NomContainer>
```
ou
```
docker container prune
```

- Suppression d'un container en cours d'execution

```
docker rm -f <IdContainer ou NomContainer>
```

- Suppression de l'ensemble des containers (en execution & arrêtés)

```
docker rm -f $(docker ps -a -q)
```
ou 

```
docker container prune -a
```

## Gestion des images

- Création une image en plaçant le dockerfile dans le répertoire courant:

```
docker build -t image-name . 
```

- Affichage liste des images
``` 
docker images
```

- Création d'un tag à la construction
```
docker build -t <dockerhub_username>/<image-name>:<tag> . 
```

- Création d'un tag pour une image après construction
```
docker image tag <src-image>:latest <dst-image>:<tag>
```

- Suppression d'une ou de plusieurs images
```
docker image rm <image-name>
```
ou
```
docker rmi <image-name>
```

- Suppression de l'ensemble des images
```
docker image prune -a
```

- Suppression des images non utilisés
```
docker image prune
```

- Suppression de l'ensemble des containers, images, réseaux, non utilisés <br>
```
docker system prune
```

- Suppression de l'ensemble des containers, images, réseaux, etc. <br>
```
docker system prune -a
```



## Persistence des données avec les volumes

- Création d'un nouveau volume pour le stockage de données

```
docker volume create <volume-name>
```

- Affichage de la liste des volumes

```
docker volume ls
```

- Affichage des informations détaillées d'un volume

```
docker volume inspect <volume-name>
```

- Configuration d'un container pour utiliser un volume

```
docker run -v <volume-name>:</path/> <container-name>
```

- Mappage d'un répertoire sur un container

```
docker run -v <local repertoire>:<chemin dans conteneur> <container-name>
```

