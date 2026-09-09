# Kubernetes Configuration

This directory contains Kubernetes manifests and configurations for deploying the application.

## Structure

- `deployment.yaml` - Kubernetes Deployment resource
- `service.yaml` - Kubernetes Service resource
- `configmap.yaml` - ConfigMap for application configuration
- `secrets.yaml` - Secrets for sensitive data
- `namespace.yaml` - Kubernetes Namespace resource
- `ingress.yaml` - Ingress for external access
- `hpa.yaml` - Horizontal Pod Autoscaler
- `pdb.yaml` - Pod Disruption Budget
- `redis-statefulset.yaml` - Redis cache with persistent storage
- `rabbitmq-statefulset.yaml` - RabbitMQ message broker with clustering
- `kong-ingress.yaml` - Kong API Gateway with ingress configuration
- `kustomization.yaml` - Kustomize configuration

## Usage

To deploy the application to Kubernetes:

```bash
# Create namespace
kubectl apply -f k8s/namespace.yaml

# Apply configurations
kubectl apply -f k8s/

# Verify deployment
kubectl get deployments -n app-namespace
kubectl get services -n app-namespace
kubectl get statefulsets -n app-namespace
kubectl get pods -n app-namespace
```

## Cleanup

```bash
kubectl delete -f k8s/
```

## Components

### Redis StatefulSet
- 3 replicas with persistent storage
- Password-protected
- LRU eviction policy
- AOF persistence enabled

### RabbitMQ StatefulSet
- 3 replicas with clustering support
- Management plugin enabled
- RBAC for cluster communication
- 20Gi persistent storage per replica

### Kong API Gateway
- 3 replicas with load balancing
- PostgreSQL backend
- Admin API and proxy endpoints
- TLS/SSL support
