# Deploy Jenkins on K8S - A simple way


- Create a namespace

```
kubectl apply -f namespace.yaml
```
- Create the deployment 

```
kubectl apply -f deployment.yaml
```
- Check if the deployment is ready

```
kubectl get deploy -n lcf-k8s-cicd
```
NB: Cette operation peut prendre du temps.

- Aficher les logs du pod Jenkins et retouver la clé secrete
```
kubectl get pod -n lcf-k8s-cicd
kubectl logs <pod_name> -n lcf-k8s-cicd
```

- Terminer la configuration en mode web
Lancer le navigateur et surfer sur l'URL http://0.0.0.0:32000

Pour la suite, nous allons configurer un noeud Kubernetes et utiliser des pods pour les operations de builds.