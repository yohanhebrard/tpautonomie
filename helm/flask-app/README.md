# Flask Application Helm Chart

Ce Helm Chart permet de déployer l'application Flask sur un cluster Kubernetes.

## Prérequis

- Kubernetes 1.19+
- Helm 3.2.0+
- Un contrôleur d'ingress installé (ex: NGINX Ingress Controller)

## Installation

```bash
# Depuis le répertoire du chart
helm install flask-app ./flask-app

# Ou en spécifiant des valeurs personnalisées
helm install flask-app ./flask-app -f values-custom.yaml
```
  
## Configuration

| Paramètre | Description | Valeur par défaut |
|-----------|-------------|-------------------|
| `replicaCount` | Nombre de réplicas du déploiement | `2` |
| `image.repository` | Repository Docker de l'image | `hebrardyohan/flask-app` |
| `image.tag` | Tag de l'image | `latest` |
| `image.pullPolicy` | Politique de récupération de l'image | `Always` |
| `service.type` | Type du service Kubernetes | `ClusterIP` |
| `service.port` | Port exposé par le service | `80` |
| `service.targetPort` | Port cible dans les pods | `8080` |
| `ingress.enabled` | Active l'ingress | `true` |
| `ingress.className` | Classe d'ingress à utiliser | `nginx` |
| `ingress.hosts` | Liste des hôtes pour l'ingress | `[{host: flask-app.local, paths: [{path: /, pathType: Prefix}]}]` |
| `resources.limits` | Limites de ressources pour les pods | `{cpu: 100m, memory: 128Mi}` |
| `resources.requests` | Requêtes de ressources pour les pods | `{cpu: 50m, memory: 64Mi}` |
| `autoscaling.enabled` | Active l'autoscaling | `false` |

## Accès à l'application

Une fois déployée, l'application sera accessible via l'ingress configuré, généralement sur l'URL `http://flask-app.local` ou via l'adresse IP externe du service LoadBalancer de l'ingress.

Pour tester localement, vous pouvez ajouter une entrée dans votre fichier `/etc/hosts` pointant `flask-app.local` vers l'adresse IP de votre ingress.