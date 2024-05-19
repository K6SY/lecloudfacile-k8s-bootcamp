## Namespace

####  Namespace basique

- Création namespace en mode declarative mode

```
kubectl create namespace k8s-lcf-01
```

- Création namespace en mode imperative 

```
kubectl create -f 01-basic-namespace.yaml
```

- Affichage des namespaces

```
kubectl get ns
```

- Clean up

```
kubectl delete namespace k8s-lcf-01 k8s-lcf-02
```

####  Exemple organisation namespace par environnement et par application

- Si vous utilisez un cluster par environnement, il est recommendé de créer un namespace par projet.

- Si vous utilisez le même cluster pour vos différentes environnements, il est recommendé de créer un namespace par environnement et par projet.

Dans cet exemple, nous considérons utiliser un même cluster pour tous les environnements.

- Création des namespaces pour une application lambda


```
kubectl apply -f 02-environment-namespace.yaml
```

- Affichage des namespaces

```
kubectl get ns --show-labels
```

- Clean Up

```
kubectl delete -f 02-environment-namespace.yaml
```

####  Gestion des ressources des namespaces

Il est important de gérer les capacités à allouer à chaque projet ou environnement pour garantir le niveau de services. En d'autres termes, certains équipes ou projet utilise plus de ressource que prévue, ce qui impacte les autres.
Kubernetes offre plusieurs mécanismes pour la gestion des ressources parmi lesquels nous pouvons noter: Quota et LimitRange.

##### Usage de ResourceQuota

ResourceQuota est une objet Kubernetes qui fournit des contraintes limitant la consommation globale de ressources par namespace. Il peut limiter la nombre d'objets qui peuvent être créés dans un namespace par type (comme l'exemple ci-desous), ainsi que la quantité totale de ressources de calcul qui peuvent être consommées par les ressources de ce namespace.

- Création d'une ResourceQuota

La commande ci-dessous permet de créer un namespace k8s-lcf-quota et une ResourceQuota qui lui sera associé et qui fixe le nombre de pod autorisé sur le namepsace à 1.

```
kubectl create -f 03-namespace-quota.yaml
```

- Affichage ResourceQuota
```
kubectl get resourcequota -n k8s-lcf-quota
```

- Création de pods pour tester

```
kubectl run quotapod1 --image=nginx -n k8s-lcf-quota

kubectl get resourcequota -n k8s-lcf-quota

kubectl run quotapod2 --image=nginx -n k8s-lcf-quota
```
Nous contatons que le premier pod quotapod1 est bien créé par contre quotapod2 ne l'est pas car le nombre pod autorisé a été atteint.

`Error from server (Forbidden): pods "quotapod2" is forbidden: exceeded quota: quota-pods, requested: pods=1, used: pods=1, limited: pods=1`

- Clean up

```
kubectl delete -f 03-namespace-quota.yaml
```

Pour plus de détails sur les ressources ResourceQuota, https://kubernetes.io/docs/concepts/policy/resource-quotas/#viewing-and-setting-quotas.

##### Usage de LimitRange

Au sein d'un namespace, un pod peut consommer autant de CPU et de mémoire que l'autorisent les ResourceQuota qui s'appliquent à cet namespace.
Une LimitRange est une politique visant à limiter les allocations de ressources (Limit et Request) que vous pouvez spécifier pour chaque type d'objet applicable (exemple pod) dans un namespace.

Pour rappel: 
*Limit*: quantité minimale d’une ressource (CPU et/ou RAM) réservée à un conteneur

*Request*: limite maximale d'une ressource (CPU et/ou RAM) que le conteneur ne peut excéder

- Création d'une LimitRange

La commande ci-dessous permet de créer un namespace k8s-lcf-limit-range et une LimitRange qui lui sera associée et qui permet de limiter les allocations de ressources aux pods.

```
kubectl create -f 04-namespace-limit-range.yaml
```

- Affichage ResourceQuota
```
kubectl get limitrange -n k8s-lcf-limit-range -o yaml
```

- Création d'un pod pour tester

```
kubectl run lrpod1 --image=nginx -n k8s-lcf-limit-range
```

- Affichage des détails du pods
```
kubectl get pod lrpod1 -n k8s-lcf-limit-range -o yaml
```

Nous pouvons constater que le container a hérité des limitations de ressources définies par la LimitRange associée au namespace.

- Création d'un pod qui dépasse les limitations

```
kubectl create -f 05-pod-out-of-limit-range.yaml
```
Le pod ne sera pas crée en raison du dépassement des limitations. Une erreur similaire sera affiché: 

`The Pod "lrpod2" is invalid: spec.containers[0].resources.requests: Invalid value: "2Gi": must be less than or equal to memory limit of 512Mi`

- Clean up

```
kubectl delete -f 04-namespace-limit-range.yaml
```


Pour plus de détails:

#https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory

#https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu

#https://kubernetes.io/docs/concepts/policy/limit-range/
