# PrometheusRule Node K8S

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* HostContextSwitching : changed threshold to 4000 based on the result during standard usage of the cluster