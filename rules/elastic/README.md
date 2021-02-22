# PrometheusRule Elastic

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* ElasticsearchNoNewDocuments (disabled because dev environment with long period of time without any document inserted)