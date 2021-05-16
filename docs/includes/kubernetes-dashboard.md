1. Install the main dashboard components:
```
GITHUB_URL=https://github.com/kubernetes/dashboard/releases
VERSION_KUBE_DASHBOARD=$(curl -w '%{url_effective}' -I -L -s -S ${GITHUB_URL}/latest -o /dev/null | sed -e 's|.*/||')
sudo k3s kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/${VERSION_KUBE_DASHBOARD}/aio/deploy/recommended.yaml
```

2. Create a dashboard user:
```
kubectl create -f kubernetes-dashboard/dashboard.admin-user.yml -f kubernetes-dashboard/dashboard.admin-user-role.yml
```

3. Get the dashboard user's token (to authenticate access to the dashboard):
```
kubectl -n kubernetes-dashboard describe secret admin-user-token | grep '^token'
```