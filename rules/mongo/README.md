# PrometheusRule Elastic

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

If you have a replicaset setup, you can add additional rules with :

```
kubectl -n monitoring apply -f ./alert_replset.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* MongodbVirtualMemoryUsage (disabled because no mapped memory in our server)

```
> db.serverStatus().mem
{ "bits" : 64, "resident" : 175, "virtual" : 1598, "supported" : true }
```

The `serveStatus.mem` is missing `mapped` information
