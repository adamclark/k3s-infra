# k3s

## Create a CentOS VM

### Create the VM
Create and power on a VM in ESXi:

| Setting | Value |
| --- | --- |
| CPU | 4 |
| Memory | 16Gb |
| DVD | CentOS Stream 8 Boot ISO |

Follow the installer and install "Server".

### Configure DNS
In Pi-hole add the following local DNS records against the server IP:

- k3s.lab
- argocd.lab
- grafana.lab
- prometheus.lab

### Enable Cockpit
`systemctl enable --now cockpit.socket`

Cockpit URL: https://k3s.lab:9090

## Install k3s

### Perform Pre-Reqs for CentOS

https://rancher.com/docs/k3s/latest/en/advanced/#additional-preparation-for-red-hat-centos-enterprise-linux

### Install k3s using the provided script:
   ```
   curl -sfL https://get.k3s.io | sh -
   ```

### Accessing the cluster using kubectl

1. Copy /etc/rancher/k3s/k3s.yaml from the k3s server to your machine as ~/.kube/config.

2. In your local copy (~/.kube/config), replace “localhost” with the IP or name of the K3s server.

### Post Installation Setup

[Install the Kubernetes Dashboard](includes/kubernetes-dashboard.md)

[Install ArgoCD](includes/argocd.md)