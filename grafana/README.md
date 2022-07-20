# grafana

> Displays charts and graphs based off of metrics (and logging) data

- [Installation](#installation)
- [Accessing](#accessing)

## Installation
```
kubectl create namespace monitoring

# ensure grafana can access all the sources needed
kubectl -n monitoring apply -f datasource-configmap.yaml

helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana -f values.yaml --namespace monitoring
```

## Accessing
1. Get your 'admin' user password by running:

```
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster _grafana.monitoring.svc.cluster.local_

Get the Grafana URL to visit by running these commands in the same shell:

```
kubectl --namespace monitoring port-forward $(kubectl get pods --namespace monitoring -l "app.kubernetes.io/name=grafana" -o jsonpath="{.items[0].metadata.name}") 3000
```

3. Login with the password from step 1 and the username `admin` on [localhost:3000](http://localhost:3000).


## Notes
- Grafana is deployed to be stateless with no persistent storage. This means that you can't create new dashboards from the UI, you can only use those that are stored in [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) created by the Helm chart. If you want to add more dashboards, you can place them in ConfigMaps.
