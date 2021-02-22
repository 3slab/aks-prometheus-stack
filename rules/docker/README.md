# PrometheusRule docker cadvisor

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* ContainerCpuUsage : add `{name!=""}` to the metric name to remove alert raised by cadvisor itself
* ContainerKilled : disabled because it raised alert for cronjob containers