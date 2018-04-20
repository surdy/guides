## How to find the number of public agents in the cluster ?

### Using DC/OS CLI
```
dcos node --json | jq '.[] | select( .attributes.public_ip == "true") | .hostname' | wc -l
```


### Using curl
```
curl -s --header "Authorization: token=<token>" http://<master-hostname-or-ip>/mesos/slaves | jq '.slaves[] | select( .attributes.public_ip == "true") | .hostname' | wc -l
```

```
curl -s --header "Authorization: token=$(dcos config show core.dcos_acs_token)" (dcos config show core.dcos_url)/mesos/slaves | jq '.slaves[] | select( .attributes.public_ip == "true") | .hostname' | wc -l
```


## How to find the IP address of the public agents in the cluster ?

```
for id in $(dcos node --json | jq --raw-output '.[] | select( .attributes.public_ip == "true") | .id'); do dcos node ssh --option StrictHostKeyChecking=no --option LogLevel=quiet --master-proxy --mesos-id=$id "hostname -i" ; done 2>/dev/null
```


## How to find the Public IP address of the public agents in the cluster ?

```
for id in $(dcos node --json | jq --raw-output '.[] | select( .attributes.public_ip == "true") | .id'); do dcos node ssh --option StrictHostKeyChecking=no --option LogLevel=quiet --master-proxy --mesos-id=$id "curl -s ifconfig.co" ; done 2>/dev/null
```
