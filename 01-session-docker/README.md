# Pratique pour la session Docker

Prérequis : 
    - Connaissance des commandes de base
    - Connaissance de la syntaxe Dockerfile
    - Docker-Desktop installé

## Lab01: Dockerization Application statique HTML

HTML est un language de balisage est le langage standard utilisé pour créer et concevoir des pages Web. Il est utilisé pour structurer le contenu d'une page Web en utilisant différents types de balises et de balisages.

- [Détails Lab](01-dockerize-static-website)


## Lab02: Dockerization Application statique PHP

PHP est un langage de programmation populaire et largement utilisé, principalement pour le développement web côté serveur.

- [Détails Lab](02-dockerize-php-app)


## Lab03: Dockerization Application Flask

[Flask](https://flask.palletsprojects.com/en/3.0.x/) est un microframework permettant le développement d'applictaion web ou d'API très rapidement.
FLask doit être déployé sur un serveur web supportant du [WSGI (Web Server Gateway Interface)](https://wsgi.readthedocs.io/en/latest/what.html). Nous allons utiliser [Guicorn](https://gunicorn.org/) qui est l'une des solutions recommendées   

- [Démarrer le Lab](03-dockerize-flask-app)


## Lab04: Déploiment d'une application avec compose

Ce lab permet de dockerizer l'application PHP lié à une base de données MYSQL avec un client phpmyadmin. L'ensemble sera déployé sous forme de service Docker-compose avec des dépendances pour garantir le bon démarrage.

- [Détails Lab](04-compose-launch-monolithic-app)

## Lab05: MKDocs pour la documentation de vos projets

L'objectif est de présenter sommairement mkdocs qui est un outil qui vous permettra de construire votre documentatin rapidement en utilisant du markdown.

Dans ce lab bonus, nous allons créer un projet de documentation que l'on va dockerizer.

- [Détails Lab](05-mkdocs-app)


## Lab06: Usage d'un reverse proxy

Si nous souhaitons exposer toutes nos applications containerisés sur le même host en utilisant les ports HTTP standard (80/443), il est possible de placer un container nginx en reverse proxy et créer des virtualhost pour chaque application.

- [Détails Lab](06-nginx-reverse-proxy)



## Lab07: Scan de vulnérabilités avec Trivy

Il est important d'incoporer très tôt les bons reflexes parmi lesquels nous pouvons noter les préoccupations sécuritaires. Dans ce lab, nous allons utiliser un scanner de vulnerabilités Trivy pour scanner les images construites.

- [Détails Lab](07-scan-vulnerabilities-trivy)

