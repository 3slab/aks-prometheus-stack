# Postgres Grafana Dashboard

Postgres uses the [postgres_exporter](https://github.com/wrouesnel/postgres_exporter).

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-postgres.yaml
```

## Changed to official dashboard

* Replace datasource reference in all the board :

   ```
   sed -i 's%"DS_PROMETHEUS",%"Prometheus",%g' grafana-dashboard-postgres.yaml
   sed -i 's%"${DS_PROMETHEUS}",%"Prometheus",%g' grafana-dashboard-postgres.yaml
   ```