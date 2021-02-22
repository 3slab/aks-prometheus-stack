## PrometheusRule (alert rules)

The default label to attach to a `PrometheusRule` to be picked up by the operator is

```
app: kube-prometheus-stack
release: monitoring
```

This is configurable in the `kube-prometheus-stack` deployment with :

```
## Namespaces to be selected for PrometheusRules discovery.
## If nil, select own namespace. Namespaces to be selected for ServiceMonitor discovery.
## See https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#namespaceselector for usage
##
ruleNamespaceSelector: {}

## If true, a nil or {} value for prometheus.prometheusSpec.ruleSelector will cause the
## prometheus resource to be created with selectors based on values in the helm deployment,
## which will also match the PrometheusRule resources created
##
ruleSelectorNilUsesHelmValues: true

## PrometheusRules to be selected for target discovery.
## If {}, select all ServiceMonitors
##
ruleSelector: {}
## Example which select all prometheusrules resources
## with label "prometheus" with values any of "example-rules" or "example-rules-2"
# ruleSelector:
#   matchExpressions:
#     - key: prometheus
#       operator: In
#       values:
#         - example-rules
#         - example-rules-2
#
## Example which select all prometheusrules resources with label "role" set to "example-rules"
# ruleSelector:
#   matchLabels:
#     role: example-rules
```

## Rules

Most of the rules are copied or inspired by the excellent [Awesome Prometheus alerts](https://awesome-prometheus-alerts.grep.to/)

* [blackbox](./blackbox/README.md)
* [coredns](./coredns/README.md)
* [docker](./docker/README.md)
* [elastic](./elastic/README.md)
* [k8s-node](./k8s-node/README.md)
* [mongo](./mongo/README.md)
* [mysql](./mysql/README.md)
* [nginx-ingress](./nginx-ingress/README.md)
* [postgres](./postgres/README.md)
* [prometheus](./prometheus/README.md)
* [rabbitmq](./rabbitmq/README.md)