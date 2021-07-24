## Install the Kubernetes Dashboard

1. Install the main dashboard components:
```
GITHUB_URL=https://github.com/kubernetes/dashboard/releases
VERSION_KUBE_DASHBOARD=$(curl -w '%{url_effective}' -I -L -s -S ${GITHUB_URL}/latest -o /dev/null | sed -e 's|.*/||')
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/${VERSION_KUBE_DASHBOARD}/aio/deploy/alternative.yaml
```

2. Create a dashboard user:
```
kubectl create -f kubernetes-dashboard/dashboard.admin-user.yml -f kubernetes-dashboard/dashboard.admin-user-role.yml
```

3. Get the dashboard user's token (to authenticate access to the dashboard):
```
kubectl -n kubernetes-dashboard describe secret admin-user-token | grep '^token'
```

## Traefik Ingress

Create ingress for the kubernetes dashboard:
```
kubectl apply -f kubernetes-dashboard/dashboard-ingress-traefik.yml
```

## NGINX Ingress
1. Install the NGINX ingress controller and wait ubtil it's running:
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