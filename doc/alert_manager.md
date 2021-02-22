# Alert Manager Configuration

The configuration can be customized using 2 different solutions :

* in the `values.yaml` file
* by creating `AlertManagerConfig` k8s resources

The alertmanager reloads automatically its configuration by merging :

* default config
* the one in the values
* all settings from `AlertManagerConfig` resources

*In case of error or your settings is not applied. Look into the prometheus operator pod log for more detail*

For more information about alert manager configuration look into [Alert manager configuration official documentation](https://prometheus.io/docs/alerting/latest/configuration/)

A more advanced documentation with the email channel is available in [Setup email channel](./alert_manager/alert_manager_email.md)

## Useful commands to send dummy alert

```
url='http://alertmanager-operated.monitoring:9093/api/v1/alerts'
echo "Firing up alert" 
curl -XPOST $url -d '[{"status": "firing","labels": {"alertname": "my_cool_alert2","service": "curl","severity": "warning","instance": "0"},"annotations": {"summary": "This is a summary","description": "This is a description."},"generatorURL": "http://prometheus.int.example.net/<generating_expression>","startsAt": "2020-07-23T01:05:36+00:00"}]'
echo ""

echo "press enter to resolve alert"
read

echo "sending resolve"
curl -XPOST $url -d '[{"status": "resolved","labels": {"alertname": "my_cool_alert2","service": "curl","severity": "warning","instance": "0"},"annotations": {"summary": "This is a summary","description": "This is a description."},"generatorURL": "http://prometheus.int.example.net/<generating_expression>","startsAt": "2020-07-23T01:05:36+00:00","endsAt": "2021-01-20T16:01:18+00:00"}]'
echo ""
```

## Summary

* [Setup email channel](./alert_manager/alert_manager_email.md)