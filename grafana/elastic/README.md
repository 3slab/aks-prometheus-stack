# Elasticsearch Grafana Dashboard

[elasticsearch_exporter](../../exporter/elastic/README.md) deployed is in version `1.1.0`.

The official repository provides this [dashboard](https://github.com/justwatchcom/elasticsearch_exporter/blob/v1.1.0/examples/grafana/dashboard.json)

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-elastic.yaml
```