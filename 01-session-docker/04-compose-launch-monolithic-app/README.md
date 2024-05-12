# Executer d'une application monolithique 3-tiers avec compose

## Démarrage des services

```
docker compose up -d
```

## Vérification des containers

```
docker ps
```

## Vérification des accès

- Pour l'application, entrer l'url http://0.0.0.0:8000

- Pour la base de données, entrer l'url http://0.0.0.0:8008 et vérifier que l'interface de phpmyadmin est bien accessible.


# Arrêt des services

```
docker compose down
```
