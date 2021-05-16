1. Install the NGINX ingress controller and wait ubtil it's running:
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.46.0/deploy/static/provider/baremetal/deploy.yaml\n

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