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
# Build and apply the Kustomize configuration
kubectl apply -k .

# Verify deployment
kubectl get deployments -n default
kubectl get services -n default
kubectl get statefulsets -n default
kubectl get pods -n default
```

## Cleanup

```bash
kubectl delete -k k8s/
```

## Components

This configuration uses one replica per workload for a small, single-node development cluster. Add node capacity and increase replica counts before using it for high availability.

### Redis StatefulSet
- 1 replica with persistent storage
- Password-protected
- LRU eviction policy
- AOF persistence enabled

### RabbitMQ StatefulSet
- 1 replica with persistent storage
- Management plugin enabled
- RBAC for cluster communication
- 20Gi persistent storage per replica

### Kong API Gateway
- 1 replica
- PostgreSQL backend
- Admin API and proxy endpoints
- TLS/SSL support
