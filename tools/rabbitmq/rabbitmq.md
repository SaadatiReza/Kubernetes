# RabbitMQ Installation with HELM
Firstly, We should install Rabbitmq operator using the below command based on the rabbitmq official documentation.
```bash
 kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"
 ```
 then make sure that the operator is up and running.
 ```bash
 kubectl get customresourcedefinitions.apiextensions.k8s.io | grep rabbit
 ```

 # Create a RabbitMQ Instance
 Then copy and paste the below snippet into the file and save it:
```yml
apiVersion: rabbitmq.com/v1beta1
kind: RabbitmqCluster
metadata:
  name: definition
```
Next, apply the definition by running:

```bash
kubectl apply -f definition.yaml
```
```bash
kubectl get all -l app.kubernetes.io/name=definition
```
NOTE: modify the word "definition" with your desired cluster name, by the way, this is not a production ready cluster and try to modify the definition with better configuration.




















 reference: 
 [reference](https://www.rabbitmq.com/kubernetes/operator/using-operator)