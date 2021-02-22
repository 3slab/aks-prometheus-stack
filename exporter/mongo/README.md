# Prometheus Mongo Exporter

The [prometheus mongodb chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-mongodb-exporter) deploys the [mongodb_exporter](https://github.com/percona/mongodb_exporter)

## Install

Create an exporter user

```
db.getSiblingDB("admin").createUser({
    user: "mongodb_exporter",
    pwd: "s3cr3tpassw0rd",
    roles: [
        { role: "clusterMonitor", db: "admin" },
        { role: "read", db: "local" },
    ]
})
```

**IMPORTANT : You need to give read access to all your project databases one at a time**

Setup the [values.yaml](./values.yaml) file

Add a metricRelabling `cluster` with the name of your mongodb cluster :

```
serviceMonitor:
  metricRelabelings:
    - targetLabel: cluster
      replacement: "mongo-k8s"
```

Install the exporter

```
helm install mongodb-exporter --version=2.8.1 --namespace=monitoring prometheus-community/prometheus-mongodb-exporter -f values.yaml  --debug --dry-run
```

## Alerts

Dedicated [PrometheusRule](../../rules/mongo/README.md) are available for this exporter.