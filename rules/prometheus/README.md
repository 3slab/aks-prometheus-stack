# PrometheusRule Prometheus

This section provides a set of alert rules to monitor Prometheus itself and the different exporters.

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* PrometheusJobMissing : renamed label to match the name of the prometheus chart when deployed
* PrometheusAlertmanagerE2eDeadManSwitch : disabled as we already have the native watchdog alert
