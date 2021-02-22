# Mongo Grafana Dashboard

Mongo uses the [mongodb_exporter](https://github.com/percona/mongodb_exporter) from percona.

Percona provides a set of dashboards in its [grafana dashboard repository](https://github.com/percona/grafana-dashboards).

The following dashboards have been extracted from commit `98924a8 on Nov 11, 2019` :

* [Overview](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_Overview.json)
* [ReplSet](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_ReplSet.json)
* [WiredTiger](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_WiredTiger.json)
* [InMemory](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_InMemory.json)
* [Cluster Summary](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_Cluster_Summary.json)
* [Nmapv1](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_MMAPv1.json)
* [RocksDB](https://github.com/percona/grafana-dashboards/blob/master/dashboards/MongoDB_RocksDB.json)

Installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-overview.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-replset.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-wiredtiger.yaml
```

Non standard dashboards for 3S installation :

```
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-cluster.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-nmapv1.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-rocksdb.yaml
kubectl -n monitoring apply -f ./grafana-dashboard-mongo-cluster.yaml
```