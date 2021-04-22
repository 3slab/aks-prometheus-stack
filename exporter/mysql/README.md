# Prometheus Mysql Exporter

The [mysql exporter chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-mysql-exporter) deploys the [mysqld_exporter](https://github.com/prometheus/mysqld_exporter)

## Install

Create an `exporter` user with limited number of connections to prevent metrics scrapping to overload the database.

```sql
CREATE USER 'exporter' IDENTIFIED BY 'jSdS7tM72y76wjfm' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter';
```

Setup the [values.yaml](./values.yaml) file

Install the exporter

```
helm install mysql-exporter --version=1.1.0 --namespace=monitoring prometheus-community/prometheus-mysql-exporter -f values.yaml  --debug --dry-run
```

## Alerts

Dedicated [PrometheusRule](../../rules/mysql/README.md) are available for this exporter.