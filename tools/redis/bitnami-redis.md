# Install  Bitnami Redis using HELM chart
First, add the bitnami repository to your system helm repository.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```
then, update your system's helm repository using below command.
```bash
helm repo update
```
download the default values of the helm chart using the below command in case of any change on default values.
```bash
helm show values bitnami/redis > values.yml
```
then, install redis instance with the modified values as follows.
```bash
helm install redis bitnami/redis -f values.yml -n redis --create-namespace
```