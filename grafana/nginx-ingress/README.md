# Nginx Ingress Grafana Dashboard

Nginx ingress provides a default metric endpoints for Prometheus out of the box if it is enabled.

The official release provides 2 dashboards :

* [General](https://github.com/kubernetes/ingress-nginx/blob/master/deploy/grafana/dashboards/nginx.json)
* [Performance](https://github.com/kubernetes/ingress-nginx/blob/master/deploy/grafana/dashboards/request-handling-performance.json)

They have been extracted from commit `117cb3b 21 days ago`.

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-nginx-ingress.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-nginx-ingress-performance.yaml
```


## Changed to official dashboard

* Rename performance dashboard to prefix `NGINX Ingress controller - ` in the title