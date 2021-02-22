# RabbitMQ Grafana Dashboard

RabbitMQ uses the [rabbitmq_exporter](https://github.com/kbudde/rabbitmq_exporter).

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-rabbitmq.yaml
```

## Changed to official dashboard

* Replace datasource reference in all the board :

   ```
   sed -i 's%"DS_PROMETHEUS",%"Prometheus",%g' grafana-dashboard-rabbitmq.yaml
   sed -i 's%"${DS_PROMETHEUS}",%"Prometheus",%g' grafana-dashboard-rabbitmq.yaml
   ```