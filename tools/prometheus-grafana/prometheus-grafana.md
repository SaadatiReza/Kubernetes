
# Install Prometheus and Grafana Stack

To install Grafana and Prometheus Stack inside your cluster follow the below instructions.


```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add grafana https://grafana.github.io/helm-charts

helm repo update

```


Next, we need to install Prometheus and Grafana using the following command:

```bash
helm install prometheus prometheus-community/prometheus
helm install grafana grafana/grafana
```

### Enable Ingress
you can enable ingress with for the prometheus with the below flag.
```bash
helm install grafana grafana/grafana --set ingress.enabled=true --set ingress.hosts='["chart-example.local"]'
```


#### NOTE
keep in mind that grafana doesn't keep data by default and in case of termination of grafana pod all the data will lose. to make the data persistence utilize below flags.

```bash
helm install grafana grafana/grafana --set persistence.enabled=true 
```
if you have any errors related to "initChownData" container, you could disable it with the below command.

```bash
helm install grafana grafana/grafana --set persistence.enabled=true --set initChownData.enabled=false
```


