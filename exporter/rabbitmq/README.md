# Prometheus RabbitMQ Exporter

The [prometheus RabbitMQ chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-rabbitmq-exporter) deploys the [rabbitmq_exporter](https://github.com/kbudde/rabbitmq_exporter)

## Install

Setup the [values.yaml](./values.yaml) file

Install the exporter

```
helm install rabbitmq-exporter --version=0.6.0 --namespace=monitoring prometheus-community/prometheus-rabbitmq-exporter -f values.yaml --debug --dry-run
```

**Alerts are bundled in the chart**