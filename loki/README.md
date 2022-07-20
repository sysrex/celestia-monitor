# Loki

> Collects application logs

```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

kubectl create namespace monitoring

helm -n monitoring install loki grafana/loki-stack -f values.yaml
```
