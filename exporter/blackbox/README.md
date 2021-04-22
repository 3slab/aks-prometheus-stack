# Prometheus Blackbox Exporter

The [prometheus blackbox chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-blackbox-exporter) deploys the [blackbox_exporter](https://github.com/prometheus/blackbox_exporter)

## Install

Setup the [values.yaml](./values.yaml) file

Install the exporter

```
helm install blackbox-exporter --version=4.11.0 --namespace=monitoring prometheus-community/prometheus-blackbox-exporter -f values.yaml --debug --dry-run
```

## Usage

This exporter is a special case. **You need to create dedicated ServiceMonitor for each page you are monitoring.**

You can use the example [ServiceMonitor](./blackbox-service-monitor.yaml) which probes google homepage.

You can do more complex use case. In [values.yaml], you can set custom config and in most of the case, add your own blackbox exporter module in replacement of the default one `http_2xx` :

```
config:
  modules:
    http_2xx:
      prober: http
      timeout: 5s
      http:
        valid_http_versions: ["HTTP/1.1", "HTTP/2.0"]
        no_follow_redirects: false
        preferred_ip_protocol: "ip4"
    http_2xx_facebook:
      prober: http
      timeout: 5s
      http:
        valid_http_versions: ["HTTP/1.1", "HTTP/2.0"]
        no_follow_redirects: false
        fail_if_body_not_matches_regexp:
          - "Avec Facebook, partagez et restez en contact avec votre entourage"
```

Then use this new module in your Service Monitor :

```
- port: http
  interval: 30s
  scrapeTimeout: 30s
  path: /probe
  params:
  target:
      - https://www.facebook.com
  module:
      - http_2xx_facebook
  metricRelabelings:
  - targetLabel: instance
    replacement: https://www.facebook.com
  - targetLabel: target
    replacement: "facebook"
```

## Alerts

Dedicated [PrometheusRule](../../rules/blackbox/README.md) are available for this exporter.