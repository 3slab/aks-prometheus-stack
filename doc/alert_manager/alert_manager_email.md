# AlertManager Email Channel

## Customize configuration in the yaml file

This is an example of configuring a default receiver channel which sends an email when an alert different from Watchdog is found (the rules on Watchdog is the default one). It sends one email per alertname and namespace. We choose to group by namespace because in our case different teams manage different namespaces. That way we could make different match routes to different receivers per namespace

Note that as we are adding a receiver in a list, we write again the default `null` receiver from the default values file because it would have been overriden by our own configuration (reminder helm does not perform deep merging on list).

```yaml
alertmanager:
  config:
    route:
      group_by: ['alertname', 'namespace']
      receiver: team-architect
    receivers:
    - name: 'null'
    - name: 'team-architect'
      email_configs:
        - to: 'architect-email@suez.com'
          from: 'monitoring@3slab.io'
          smarthost: 'smtp.sendgrid.net:25'
          auth_username: apikey
          auth_password: '<my_api_key>'
          headers:
            subject: '[3slab-k8s-dev] {{ template "__subject" . }}'
          send_resolved: true
```

It generates the following configuration in alert manager :

```yaml
global:
  resolve_timeout: 5m
route:
  receiver: team-architect
  group_by:
  - alertname
  - namespace
  routes:
  - receiver: "null"
    match:
      alertname: Watchdog
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
receivers:
- name: "null"
- name: team-architect
  email_configs:
  - to: architect-email@suez.com
    from: monitoring@3slab.io
    smarthost: smtp.sendgrid.net:25
    auth_username: apikey
    auth_password: <my_api_key>
    headers:
      subject: '[3slab-k8s-dev] {{ template "__subject" . }}'
    send_resolved: true
templates: []
```

## Use an AlertManagerConfig resource

You have an example of the [AlertManagerConfig resource](../../alertmanager/alertmanager-email.yaml)

This resource generates the following configuration.

**IMPORTANT : it creates a route which match the namespace where the resource was found and THIS CANNOT BE OVERRIDEN** so it could be useful to handle different receiver per namepace.

```yaml
global:
  resolve_timeout: 5m
route:
  receiver: "null"
  group_by:
  - job
  routes:
  - receiver: monitoring-send-all-alerts-to-architect-team-architect
    group_by:
    - alertname
    - namespace
    match:
      namespace: monitoring
    continue: true
  - receiver: "null"
    match:
      alertname: Watchdog
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 12h
receivers:
- name: "null"
- name: monitoring-send-all-alerts-to-architect-team-architect
  email_configs:
  - to: architect-email@suez.com
    from: monitoring@3slab.io
    smarthost: smtp.sendgrid.net:25
    auth_username: apikey
    auth_password: |
      <my_api_key>
```