kubectl create ns json-exporter
helm install json-exporter prometheus-community/prometheus-json-exporter -n json-exporter -f values.yml
