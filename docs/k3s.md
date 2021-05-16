# k3s

## Install k3s

### Install k3s using the provided script:
   ```
   curl -sfL https://get.k3s.io | sh -
   ```

### Accessing the cluster using kubectl

1. Copy /etc/rancher/k3s/k3s.yaml from the k3s server to your machine as ~/.kube/config.

2. In your local copy (~/.kube/config), replace “localhost” with the IP or name of the K3s server.

## Install the Kubernetes Dashboard

@@include[kubernetes-dashboard.md](includes/kubernetes-dashboard.md)

## Setup NGINX Ingress

@@include[nginx-dashboard-ingress.md](includes/nginx-dashboard-ingress.md)

## Install ArgoCD

@@include[argocd.md](includes/nginx-dashboard-ingress.md)