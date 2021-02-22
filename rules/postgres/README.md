# PrometheusRule Postgres

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

If you have a master/slave setup, you can add additional rules with :

```
kubectl -n monitoring apply -f ./alert_slave.yaml
```

## Alerts

Some alerts have been disabled or changed to match the behavior of our applications. Don't forget to adapt the rules to your environment.

Changed or disabled alert rules :

* PostgresqlNotEnoughConnections (our application does not maintain a permanent connection)
* PostgresqlHighRollbackRate (2% per default too small because our ORM rollback transaction it does not need to execute. Changed to 5%)
* PostgresqlCommitRateLow (this is a dev cluster so the commited transaction rate is slow. Changed to validate that it is not 0)