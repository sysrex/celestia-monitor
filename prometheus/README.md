# prometheus

> A monitoring and alerting service

```
kubectl create namespace monitoring
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus --namespace monitoring -f prometheus/values.yaml
```

Accessing the instance on [localhost:8082](http://localhost:8082):
```
kubectl --namespace monitoring port-forward service/prometheus-server 8082:80
```
