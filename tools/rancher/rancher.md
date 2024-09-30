# Add the Helm Chart Repository
```bash
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
```

# Create a Namespace for Rancher
```bash
kubectl create namespace cattle-system
```

# Install cert-manager
```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update

helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true
```
# Install Rancher with Helm
```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.my.org \
  --set bootstrapPassword=admin
```

# Troubleshoot
if your pod continously being restarted, it might be related to liveness and readiness prob. try disable it temporarily to see the result.

if you wish to ignore setting up ssl inside your cluster (for the communication of your pod to rancher), you can offload ssl in your ingress controller with adding bellow option.

```bash
helm install rancher rancher-stable/rancher \
  --namespace cattle-system \
  --set hostname=rancher.milad.com \
  --set bootstrapPassword=admin \
  --set tls=external
```
