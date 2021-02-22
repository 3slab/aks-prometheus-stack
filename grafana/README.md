# Grafana

[Grafana](https://grafana.com/) provides dashboards to visualize metrics pulled by Prometheus. A lot of default dashboards are already registered when installing the Prometheus stack but you can provide your own.

## Dashboards

* [elastic](./elastic/README.md)
* [kong](./kong/README.md)
* [mongo](./mongo/README.md)
* [mysql](./mysql/README.md)
* [nginx-ingress](./nginx-ingress/README.md)
* [postgres](./postgres/README.md)
* [rabbitmq](./rabbitmq/README.md)

## Create a K8S Grafana Dashboard resource

A Grafana dashboard k8s resource is a ConfigMap containing one or multiples json files with a label `grafana_dashboard` equals to `1`.

Exemple :

```
apiVersion: v1
data:
  my-dashboard.json: |-
    {
        "__inputs": [

        ],
        "__requires": [

        ],
        "annotations": {
            "list": [

            ]
        },
        "editable": false,
        "gnetId": null,
        "graphTooltip": 0,
        "hideControls": false,
        "id": null,
        "links": [

        ],
        "panels": [
            ...
        ],
        "schemaVersion": 14,
        "style": "dark",
        "tags": [
            ...
        ],
        "templating": {
            "list": [
                ...
            ]
        },
        "time": {
            "from": "now-1h",
            "to": "now"
        },
        "timepicker": {
            "refresh_intervals": [
                "5s",
                "10s",
                "30s",
                "1m",
                "5m",
                "15m",
                "30m",
                "1h",
                "2h",
                "1d"
            ],
            "time_options": [
                "5m",
                "15m",
                "1h",
                "6h",
                "12h",
                "24h",
                "2d",
                "7d",
                "30d"
            ]
        },
        "timezone": "UTC",
        "title": "<dashboard name>",
        "uid": "<dashboard uuid>",
        "version": 0
    }
kind: ConfigMap
metadata:
  labels:
    grafana_dashboard: "1"
  name: monitoring-grafana-my-dashboard
  namespace: monitoring
```

Grafana pods has a sidecar which watches the kubernetes event stream and react when a new configmap for a dashboard is detected. However, in its version `1.1.0`, it gets a ConnectionRefused 104 connection closed by peer error and does not reload automaticaly the dashboards configuration. So you will need to force a restart of the grafana pod after each new dashboard addition :

```
kubectl -n monitoring delete pod `kubectl -n monitoring get pods -l app.kubernetes.io/name=grafana -o jsonpath={..metadata.name}`
```