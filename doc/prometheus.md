# Prometheus

THe prometheus stack in K8S uses an operator which query the K8S api to get information about which endpoints, rules and alerts it needs to handle. These information are setup with custom dedicated K8S resources like `ServiceMonitor`.

More information in the [getting started](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/user-guides/getting-started.md) documentation

## ServiceMonitor

See dedicated doc about [ServiceMonitor and exporter](../exporter/README.md)

## PrometheusRules

See dedicated doc about [PrometheusRule](../rules/README.md)
