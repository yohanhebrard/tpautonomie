# Commandes d'installation des charts Helm

## Installation de NGINX Ingress Controller

```bash
# Ajouter le repository Bitnami
helm repo add bitnami https://charts.bitnami.com/bitnami

# Mettre à jour les repositories Helm
helm repo update

# Installer NGINX Ingress Controller
helm install nginx-ingress bitnami/nginx-ingress-controller \
  --namespace ingress-nginx \
  --create-namespace \
  --set service.type=LoadBalancer
```

## Installation de Kubecost

```bash
# Ajouter le repository Mesosphere
helm repo add mesosphere-stable https://mesosphere.github.io/charts/stable

# Mettre à jour les repositories Helm
helm repo update

# Installer Kubecost
helm install kubecost mesosphere-stable/kubecost \
  --namespace kubecost \
  --create-namespace
```

## Vérifier les installations

```bash
# Vérifier le statut de l'Ingress Controller
kubectl get pods -n ingress-nginx

# Vérifier le statut de Kubecost
kubectl get pods -n kubecost

# Obtenir l'adresse IP externe de l'Ingress Controller
kubectl get services -n ingress-nginx
```

## Installation de notre application Flask

```bash
# Installation de l'application Flask
helm install flask-app ./helm/flask-app \
  --namespace default \
  --create-namespace
```

## Vérifier le déploiement de l'application

```bash
# Vérifier les pods de l'application
kubectl get pods

# Vérifier le service
kubectl get services

# Vérifier l'ingress
kubectl get ingress
```