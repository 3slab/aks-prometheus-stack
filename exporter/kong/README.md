# Prometheus Kong Exporter

Kong comes with a native [Prometheus plugin](https://docs.konghq.com/hub/kong-inc/prometheus/).
Once the plugin is enabled, you just need to setup a service monitor to it.

## Install

1. Enable the plugin. You have 2 solutions :

    * In the kong chart. It should be enabled by default if you did not change the plugin section with the value `bundled`.

    * By calling the admin API to enable the plugin :

        ```
        $ curl -X POST http://<admin-hostname>:8001/plugins/ \
            --data "name=prometheus" 
        ```

2. Install the ServiceMonitor to let prometheus operator collects the Kong metrics endpoint. Here 2 solutions also :

    * In the kong chart. You can deploy the ServiceMonitor bundled with the chart :

        ```
        serviceMonitor:
        enabled: true
        # interval: 10s
        # Specifies namespace, where ServiceMonitor should be installed
        namespace: monitoring
        labels:
            release: monitoring
        ```

    * Create your own ServiceMonitor using this [example kong service monitor file](./kong-service-monitor.yaml)

        ```
        kubectl -n monitoring apply -f kong-service-monitor.yaml
        ```

**The service monitor needs to live in the SAME namespace as the service you want to monitor or if you prefer to reference it in the monitoring namespace, you need to add a namespaceSelector inside the ServiceMonitor definition**