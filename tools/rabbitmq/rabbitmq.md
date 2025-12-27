# RabbitMQ Installation with HELM
First, install the RabbitMQ Cluster Operator using the following command, based on the official RabbitMQ documentation:
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
Replace the word *"definition"* with your desired cluster name. Also, be aware that this configuration is not production-ready. For production use, you should extend and modify the definition with more appropriate and robust settings.



















 reference: 
 [reference](https://www.rabbitmq.com/kubernetes/operator/using-operator)