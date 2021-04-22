# Prometheus ElasticSearch Exporter

The [prometheus Elasticsearch chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-elasticsearch-exporter) deploys the [elasticsearch_exporter](https://github.com/justwatchcom/elasticsearch_exporter)

## Install

Setup the [values.yaml](./values.yaml) file

Add a metricRelabling `cluster` with the name of your elastic cluster :

```
serviceMonitor:
  metricRelabelings:
    - targetLabel: cluster
      replacement: "elastic-k8s"
```

Install the exporter

```
helm install elasticsearch-exporter --version=4.4.0 --namespace=monitoring prometheus-community/prometheus-elasticsearch-exporter -f values.yaml --debug --dry-run
```

## Alerts

Dedicated [PrometheusRule](../../rules/elastic/README.md) are available for this exporter.