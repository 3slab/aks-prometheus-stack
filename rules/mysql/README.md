# PrometheusRule MySQL

Enable alerting rules :

```
kubectl -n monitoring apply -f ./alert_base.yaml
```

If you have a master/slave setup, you can add additional rules with :

```
kubectl -n monitoring apply -f ./alert_slave.yaml
```

## Troubleshooting

### SSL Connection

In case of a database with mandatory SSL connection, you can add the param `tls=skip-verify` to the mysql datasource uri. Current [values.yml](./values.yaml) file has been setup with this setting.
