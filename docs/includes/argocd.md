## Install ArgoCD

Install ArgoCD:

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Traefik Ingress

Ensure that `argocd` is configured in DNS to resolve to the k3s server's IP address. Create ingress for Argocd:

```
kubectl apply -f argocd/traefik-argocd-ingress.yml
```
## NGINX Ingress

Ensure that `argocd` is configured in DNS to resolve to the k3s server's IP address. Create ingress for Argocd:

```
kubectl apply -f argocd/nginx-argocd-ingress.yml
```