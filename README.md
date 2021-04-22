# AKS Prometheus Stack

This repository provides a guideline with base settings to enable the prometheus stack on AKS

It uses the helm chart [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) as its core.

**Current documentation done with chart version 15.1.3. It needs k8s >= 1.19.**

## Installation

1. Enable helm repository

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

2. Create a `monitoring` namespace

```
kubectl create namespace monitoring
```

3. Update `values.yaml` file to match your custom configuration. All changes from default in this repository have been marked with a command `# ---AKS---`

Elements changed :

* Disable all monitoring of non accessible master element in AKS
* Add persistent volumes with managed premium

4. Create basic auth secrets for ingress public exposition

```
export PROMETHEUS_SECRET=`openssl rand -base64 32`
echo "prometheus:$PROMETHEUS_SECRET" > ./basic-auth/prometheus-auth.clear
htpasswd -bc ./basic-auth/prometheus-auth prometheus $PROMETHEUS_SECRET

export GRAFANA_SECRET=`openssl rand -base64 32`
echo "grafana:$GRAFANA_SECRET" > ./basic-auth/grafana-auth.clear
htpasswd -bc ./basic-auth/grafana-auth grafana $GRAFANA_SECRET

export ALERTMANAGER_SECRET=`openssl rand -base64 32`
echo "alertmanager:$ALERTMANAGER_SECRET" > ./basic-auth/alertmanager-auth.clear
htpasswd -bc ./basic-auth/alertmanager-auth alertmanager $ALERTMANAGER_SECRET

kubectl -n monitoring delete secret basic-auth-prometheus
kubectl -n monitoring create secret generic basic-auth-prometheus --from-file=auth=basic-auth/prometheus-auth
kubectl -n monitoring delete secret basic-auth-grafana
kubectl -n monitoring create secret generic basic-auth-grafana --from-file=auth=basic-auth/grafana-auth
kubectl -n monitoring delete secret basic-auth-alertmanager
kubectl -n monitoring create secret generic basic-auth-alertmanager --from-file=auth=basic-auth/alertmanager-auth
```

5. Create your own project `values_myproject.yaml` file with dedicated settings like secrets or ingress.

**WARNING : HELM DOES NOT PERFORM DEEP MERGING OF DIFFERENT VALUES FILES. SO YOU NEED TO REPEAT PART OF BASE CONF IF YOU UPDATE LIST ITEMS FOR EXAMPLE**

6. Install the prometheus stack

```
helm install --namespace=monitoring monitoring prometheus-community/kube-prometheus-stack --version=15.1.3 -f values.yaml -f values_myproject.yaml --dry-run --debug
```

*Remove the dry run and debug when you have reviewed what helm is going to deploy*

## Advanced

* [Alert manager configuration](./doc/alert_manager.md)
    * [Example with an email channel](./doc/alert_manager/alert_manager_email.md)
* [Prometheus Operator](./doc/prometheus.md)
    * [Exporters](./exporter/README.md) :
        * [blackbox](./exporter/blackbox/README.md)
        * [elastic](./exporter/elastic/README.md)
        * [kong](./exporter/kong/README.md)
        * [mongodb](./exporter/mongo/README.md)
        * [mysql](./exporter/mysql/README.md)
        * [nginx-ingress](./exporter/nginx-ingress/README.md)
        * [postgres](./exporter/postgres/README.md)
        * [rabbitmq](./exporter/rabbitmq/README.md)
    * [Rules](./rules/README.md) :
        * [blackbox](./rules/blackbox/README.md)
        * [coredns](./rules/coredns/README.md)
        * [docker](./rules/docker/README.md)
        * [elastic](./rules/elastic/README.md)
        * [k8s-node](./rules/k8s-node/README.md)
        * [mongo](./rules/mongo/README.md)
        * [mysql](./rules/mysql/README.md)
        * [nginx-ingress](./rules/nginx-ingress/README.md)
        * [postgres](./rules/postgres/README.md)
        * [prometheus](./rules/prometheus/README.md)
        * [rabbitmq](./rules/rabbitmq/README.md)
* [Grafana](./grafana/README.md)
    * [elastic](./grafana/elastic/README.md)
    * [kong](./grafana/kong/README.md)
    * [mongo](./grafana/mongo/README.md)
    * [mysql](./grafana/mysql/README.md)
    * [nginx-ingress](./grafana/nginx-ingress/README.md)
    * [postgres](./grafana/postgres/README.md)
    * [rabbitmq](./grafana/rabbitmq/README.md)

## Testing

During testing, I use two non commited `values_test.yaml` and `values_myproject.yaml` files with settings I don't want to end in the repository. So my commands are :

```
helm install --namespace=monitoring monitoring prometheus-community/kube-prometheus-stack --version=13.0.2 -f values.yaml -f values_myproject.yaml -f values_test.yaml --dry-run --debug
```