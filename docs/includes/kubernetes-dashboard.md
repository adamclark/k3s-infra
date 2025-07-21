## Install the Kubernetes Dashboard

1. Install the main dashboard components:
```
# Add kubernetes-dashboard repository
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
# Deploy a Helm Release named "kubernetes-dashboard" using the kubernetes-dashboard chart
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard
```

2. Create a dashboard user:
```
kubectl create -f kubernetes-dashboard/dashboard.admin-user.yml -f kubernetes-dashboard/dashboard.admin-user-role.yml
```

3. Create a token for the dashboard user (to authenticate access to the dashboard):
```
kubectl -n kubernetes-dashboard create token admin-user
```

## Traefik Ingress

Create insecure transport (skip tls verification) for the kubernetes dashboard:
```
kubectl apply -f kubernetes-dashboard/insecure-server-transport.yml
```

Create ingress for the kubernetes dashboard:
```
kubectl apply -f kubernetes-dashboard/dashboard-ingress-traefik.yml
```

## NGINX Ingress
1. Install the NGINX ingress controller and wait until it's running:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.46.0/deploy/static/provider/baremetal/deploy.yaml

kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
```

2. Edit the ingress controller deployment to add command line argument `--enable-ssl-passthrough` (required for argocd).
```
kubectl edit deployment ingress-nginx-controller -n ingress-nginx
```

3. Ensure that k3s.lab is configured in DNS to resolve to the k3s server's IP address. Create ingress for kubernetes dashboard:
```
kubectl apply -f kubernetes-dashboard/dashboard-ingress-nginx.yml
```
