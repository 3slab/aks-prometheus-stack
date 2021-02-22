# Prometheus Nginx Ingress Exporter

The [nginx ingress chart](https://github.com/kubernetes/ingress-nginx/tree/master/charts/ingress-nginx) already has a Prometheus metric endpoint available. It can be referenced as a target in Prometheus to be collected.

## Install

1. Install nginx ingress chart with metrics enabled. In the official chart, you just need to setup these settings :

    ```
    controller:
      metrics:
        enabled: true
      stats:
        enabled: true
    ```

    Or in the commande line :

    ```
    --set controller.metrics.enabled=true \
    --set controller.stats.enabled=true \
    ```

2. Then you need to tell Prometheus to collect nginx metrics thanks to a ServiceMonitor. 2 solutions :

    1. Use the one from the official chart :

        ```
        metrics:
          serviceMonitor:
            enabled: true
            additionalLabels:
              release: monitoring
            namespace: monitoring
            namespaceSelector:
               any: true
        ```

    2. Create a custom service monitor. Look at [./nginx-ingress-service-monitor.yaml] for an example

        ```
        kubectl -n monitoring apply -f ./nginx-ingress-service-monitor.yaml
        ```

## Alerts

Dedicated [PrometheusRule](../../rules/nginx-ingress/README.md) are available for this exporter.