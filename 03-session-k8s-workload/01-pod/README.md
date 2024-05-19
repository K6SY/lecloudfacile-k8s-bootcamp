## Pod

####  Pod basic avec un container nginx

- Création pod en mode imperative mode

```
kubectl run pod01-nginx --image=nginx
```

- Création pod en mode declarative 

```
kubectl create -f 01-basic-pod.yaml
```

NB: Il est possible de générer le manifest d'un pod à partir d'une commande kubectl.

```
kubectl run pod03-nginx --image=nginx -o yaml --dry-run=client > pod03.yaml
```

- Affichage des pods

```
kubectl get pods -o wide
```

- Affichage des pods en affichant les labels

```
kubectl get pods --show-labels
```

- Accès au pod depuis la machine local avec **kubectl port-forward**

**kubectl port-forward** permet d'établir un tunnel sécurisé entre la machine locale et un pod au sein du cluster. Cette méthode est utile pour le débogage et le développement.

La commande ci-dessous permet de rediriger les requêtes sur le port local 8088 de votre machine vers le port 80 du pod pod01-nginx

```
kubectl port-forward pod/pod01-nginx 8088:80
```

NB: Nous allons dans la suite utiliser les services pour la gestion des accès.

- Clean up

```
kubectl delete pods pod01-nginx pod02-nginx
```

#### Définition des ressources minimale d'un pod

L’objectif principal consiste à réglementer l’usage des ressources pour chaque conteneur du pod telles que le CPU et la RAM. Il est formalisé par l’ajout d’une section ressource dans le manifeste kubernetes et spécifie:

La demande de ressource (Resource Request): quantité minimale d’une ressource réservée à un conteneur

La limitation de ressource (Resource Limit): limite maximale d'une ressource que
le conteneur ne peut excéder.

La spécification ci-dessous traduit un exemple d’utilisation concret:

Resource Request : CPU = 500m / RAM = 512Mi

Resource Limit: CPU = 1000m / 2048 Mi

- Création d'un pod avec limitation de ressources

```
kubectl create -f 02-pod-resources-memory-cpu.yaml
```

- Desciption du pods

```
kubectl describe pod/pod-resources-memory-cpu
```

- Clean up

```
kubectl delete -f 02-pod-resources-memory-cpu.yaml
```

