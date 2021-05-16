# k3os

## Install k3os

Create a VM and mount the [k3os ISO](https://github.com/rancher/k3os/releases) to boot from.

After the VM has booted from the ISO login as user `rancher` and install k3os to disk:

```sudo k3os install```

When prompted during installation add your GitHub ID so that you can SSH onto the VM after installation using:

```ssh rancher@<hostname>```

Configure DNS so that  `hostname` resolves to the IP address of the VM.

### Accessing the cluster using kubectl

1. Copy /etc/rancher/k3s/k3s.yaml from the k3s server to your machine as ~/.kube/config.

```scp rancher@<hostname>:/etc/rancher/k3s/k3s.yaml ~/.kube/config```

2. In your local copy (~/.kube/config), replace “localhost” with the IP or hostname of the K3s server.

## Install the Kubernetes Dashboard

@@include[kubernetes-dashboard.md](includes/kubernetes-dashboard.md)

## Setup Traefik Ingress

@@include[traefix-dashboard-ingress.md](includes/traefix-dashboard-ingress.md)

## Install ArgoCD

@@include[argocd.md](includes/nginx-dashboard-ingress.md)