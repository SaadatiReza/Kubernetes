kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.2/deploy/static/provider/cloud/deploy.yaml

#if you want your ingress nodeport, you must modify it's configuration as belows.

First, you need to retrieve the YAML configuration of the existing LoadBalancer service.

kubectl get svc <service-name> -o yaml > service.yaml


