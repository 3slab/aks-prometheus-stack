# Kong Grafana Dashboard

Kong use its [Prometheus plugin](https://docs.konghq.com/hub/kong-inc/prometheus/) to expose metrics. The plugin provides this [dashboard](https://grafana.com/grafana/dashboards/7424)

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-kong.yaml
```

## Changed to official dashboard

* Replace datasource reference in all the board :

   ```
   sed -i 's%"DS_PROMETHEUS",%"Prometheus",%g' grafana-dashboard-kong.yaml
   sed -i 's%"${DS_PROMETHEUS}",%"Prometheus",%g' grafana-dashboard-kong.yaml
   ```