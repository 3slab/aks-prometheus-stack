# Prometheus Postgres Exporter

The [prometheus postgres chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-postgres-exporter) deploys the [postgres_exporter](https://github.com/wrouesnel/postgres_exporter)

## Install

**IMPORTANT : the [settings](https://github.com/wrouesnel/postgres_exporter#running-as-non-superuser) to use non root user changes postgres standard views which cannot be done in cloud managed database. So we use the postgres admin user in the exporter**

Setup the [values.yaml](./values.yaml) file

Install the exporter

```
helm install postgres-exporter --version=2.3.0 --namespace=monitoring prometheus-community/prometheus-postgres-exporter -f values.yaml --debug --dry-run
```

## Alerts

Dedicated [PrometheusRule](../../rules/postgres/README.md) are available for this exporter.