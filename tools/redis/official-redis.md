# Install Official Redis using HELM chart
First, Pull the latest version of the operator bundle:
```bash
VERSION=`curl --silent https://api.github.com/repos/RedisLabs/redis-enterprise-k8s-docs/releases/latest | grep tag_name | awk -F'"' '{print $4}'`
```

## Deploy the operator bundle 
Apply the operator bundle in your REC namespace:
don't forget to change the below namespace if you want to install redis on a namespace rather than redis.
```bash
kubectl apply -f https://raw.githubusercontent.com/RedisLabs/redis-enterprise-k8s-docs/$VERSION/bundle.yaml -n redis
```

```bash
cat <<EOF > my-rec.yaml
apiVersion: "app.redislabs.com/v1"
kind: "RedisEnterpriseCluster"
metadata:
  name: my-rec
spec:
  nodes: 3
EOF
```
```bash
kubectl apply -f my-rec.yaml
```











 [Refference](https://redis.io/docs/latest/operate/kubernetes/deployment/quick-start/)