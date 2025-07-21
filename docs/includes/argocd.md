## Install ArgoCD

Install ArgoCD:

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Disable TLS (ingress will still be via HTTPS)
Configure ArgoCD to start with the `--insecure` option as described [here](https://rtfm.co.ua/en/argocd-an-overview-ssl-configuration-and-an-application-deploy/#ArgoCD_SSL_ERR_TOO_MANY_REDIRECTS).

UPDATE: This is now acheived by adding the following to the argocd-cmd-params-cm ConfigMap:
```
{
	"server.insecure": "true"
}
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
