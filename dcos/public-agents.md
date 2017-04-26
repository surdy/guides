## How to find the number of public agents in the cluster ?

### Using DC/OS CLI
```
dcos node --json | jq '.[] | select(.reserved_resources.slave_public != null) | [.id] | length'
```

### Using curl
```
curl -s --header "Authorization: token=<token>" http://<master-hostname-or-ip>/mesos/slaves | jq '.slaves[] | select(.reserved_resources.slave_public != null) | [.id] | length'
```

```
curl -s --header "Authorization: token=$(dcos config show core.dcos_acs_token)" (dcos config show core.dcos_url)/mesos/slaves | jq '.slaves[] | select(.reserved_resources.slave_public == null) | [.id] | length'
```


## How to find the IP address of the public agents in the cluster ?

```
for id in $(dcos node --json | jq --raw-output '.[] | select(.reserved_resources.slave_public != null) | .id'); do dcos node ssh --option StrictHostKeyChecking=no --option LogLevel=quiet --master-proxy --mesos-id=$id "hostname -i" ; done 2>/dev/null
```


## How to find the Public IP address of the public agents in the cluster ?

```
for id in $(dcos node --json | jq --raw-output '.[] | select(.reserved_resources.slave_public != null) | .id'); do dcos node ssh --option StrictHostKeyChecking=no --option LogLevel=quiet --master-proxy --mesos-id=$id "curl -s ifconfig.co" ; done 2>/dev/null
```
