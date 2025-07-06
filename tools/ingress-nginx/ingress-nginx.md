
# Ingress-Nginx

At first you should deploy your project with the below command on your cluster.


### **Note:** You should retrieve the latest stable version and place in the below segment to make sure that you will be installing the latest version of the application.
```bash
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/cloud/deploy.yaml --namespace ingress-nginx
```

Now you can make sure that your ingress is up and running with the below command.

```bash
kubectl get pod -n ingress-nginx
```

# Change Loadbalancer service into Nodeport
If you want to change the type of your ingress service from Loadbalancer to Nodeport follow the below instruction.

### 1. Get the Current Service Definition
Replace <service-name> with the name of your service.
```bash
kubectl get svc <service-name> -o yaml > service.yaml
```
### 2. Edit the Service YAML

Then, open the service.yaml file in a text editor and look for the type field under spec. It should currently be set to LoadBalancer. Change it to NodePort:

```yaml
spec:
  type: NodePort
```
### 3. Apply the Changes

Once you've made the changes, you can apply the updated YAML configuration to the Kubernetes cluster:

```bash
kubectl apply -f service.yaml
```
