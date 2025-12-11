### Logging Operator
Firstly, you should install the loggin operator using the below command.
```bash
helm upgrade --install --wait --create-namespace --namespace logging logging-operator oci://ghcr.io/kube-logging/helm-charts/logging-operator --set logging.enabled=true
```
# Create secret for elasticsearch usage
```bash
 kubectl create secret generic elastic-credentials   --from-literal=username="example"   --from-literal=password="example"   -n production
 ```