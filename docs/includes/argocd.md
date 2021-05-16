

Install ArgoCD:

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Ensure that `argocd` is configured in DNS to resolve to the k3s server's IP address. Create ingress for Argocd:

```
kubectl apply -f argocd/argocd-ingress.yml
```