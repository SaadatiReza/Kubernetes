# Logging Operator
Firstly, you should install the loggin operator using the below command.
```bash
helm upgrade --install --wait --create-namespace --namespace logging logging-operator oci://ghcr.io/kube-logging/helm-charts/logging-operator --set logging.enabled=true
```
### Create secret for elasticsearch usage
```bash
 kubectl create secret generic elastic-credentials   --from-literal=username="example"   --from-literal=password="example"   -n production

 ```

# Increase Resource and Limit for cpu and memory 
```yml
apiVersion: logging.banzaicloud.io/v1beta1
kind: Logging
metadata:
spec:
  clusterDomain: cluster.local # if you have a different name for your cluster, change this parametere.
  controlNamespace: logging
  fluentd:
    bufferStorageVolume:
      pvc: {}
    resources:
      limits:
        cpu: 2
        memory: 2096M
      requests:
        cpu: 500m
        memory: 100M
status:
  watchNamespaces:
  - '*'
```

