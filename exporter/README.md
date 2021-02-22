# Exporter and ServiceMonitor

## ServiceMonitor

The default label to attach to a `ServiceMonitor` to be picked up by the operator is

```
release: monitoring
```

This is configurable in the `kube-prometheus-stack` deployment with :

```
serviceMonitorSelector: {}
## Example which selects ServiceMonitors with label "prometheus" set to "somelabel"
# serviceMonitorSelector:
#   matchLabels:
#     prometheus: somelabel

## Namespaces to be selected for ServiceMonitor discovery.
##
serviceMonitorNamespaceSelector: {}
## Example which selects ServiceMonitors in namespaces with label "prometheus" set to "somelabel"
# serviceMonitorNamespaceSelector:
#   matchLabels:
#     prometheus: somelabel
```

## Exporters

* [blackbox](./blackbox/README.md)
* [elastic](./elastic/README.md)
* [kong](./kong/README.md)
* [mongodb](./mongo/README.md)
* [mysql](./mysql/README.md)
* [nginx-ingress](./nginx-ingress/README.md)
* [postgres](./postgres/README.md)
* [rabbitmq](./rabbitmq/README.md)
