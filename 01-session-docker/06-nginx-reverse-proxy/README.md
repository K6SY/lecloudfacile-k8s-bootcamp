

En déploiement plusieurs applications via docker-compose, il faudra prévoir à exposer certains containers sur la machine hôte pour qu'il soit accessible. En voulant utiliser les ports classiques http (80/443), je ne peux exposer qu'un seul container.

Avec l'usage d'un reverse-proxy, je pourrai exposer un seul container proxy sur les ports 80/443 de la machine hôte. Ce container contiendra des règles de redirection vers les autres containers qui ne seront pas exposés. Ainsi toutes les requêtes quelques soit l'application, transite par le container proxy qui se chargera de le rediriger vers le bon conteneur applicatif.

#### nettoyage de l'environnement de Lab

```
docker system prune -a
```

#### Ajouter les entrées DNS dans le fichier hosts

```
127.0.0.1 flask-app.lab.io
127.0.0.1 php-app.lab.io
127.0.0.1 doc.lab.io
```


#### Créer un réseau docker

```
docker network create mynetwork
```

#### Vérifier que le réseau est bien créé

```
docker network ls --filter name=mynetwork
docker network inspect mynetwork 
```

#### Executer des containers applicatifs 
```
docker run --network mynetwork --name myawesome-flask-app -d flaskapp
docker run --network mynetwork --name myawesome-php-app -d phpapp
docker run --network mynetwork --name myawesome-doc-app -d docapp
```

#### Vérifier que les containers ont bien démarrés
```
docker ps --filter name=myawesome-flask-app
docker ps --filter name=myawesome-php-app
docker ps --filter name=myawesome-doc-app
```

#### Démarrer le reverse proxy

```
docker compose up -d
```


### Vérifier la bonne execution

```
http://flask-app.lab.io/
http://php-app.lab.io/
http://doc.lab.io/
```

