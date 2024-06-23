
# Nginx Ingress

- Deploy nginx controller

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml

- check if all components are deployed

```
kubectl get all -n ingress-nginx
```

- Create a deployment for test

```
kubectl apply -f app.yaml
```

- Create a service 

```
kubectl apply -f service.yaml
```

- Create an ingress

```
kubectl apply -f ingress.yaml
```

- Add an entry to /etc/hosts file

127.0.0.1 --> myingress.lcf.io

- Check if all is ok

navigate to http://myingress.lcf.io


- Create a certificate with let's encrypt



# ArgoCD

- Install argocd
```
kubectl create namespace argocd
kubectl apply -n argocd -f install-argo.yaml
```

NB: we add " server.insecure: 'true' " to the configmap argocd-cmd-params-cm

- Get secret password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d




https://cert-manager.io/docs/installation/

