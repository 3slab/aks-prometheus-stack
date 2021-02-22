# Mysql Grafana Dashboard

Mysql uses the [mysqld_exporter](https://github.com/prometheus/mysqld_exporter).

An [officiel dashboard](https://github.com/prometheus/mysqld_exporter/blob/master/mysqld-mixin/dashboards/mysql-overview.json) is available with the exporter. It has been extracted from commit `b8373d4 on Oct 20, 2020`.

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-mysql.yaml
```