## How to find out the version of DC/OS ?

### From cluster node
```
cat /opt/mesosphere/active/dcos-metadata/etc/dcos-version.json
```
OR
```
cat /opt/mesosphere/etc/dcos-version.json
```

### Using DC/OS CLI
```
dcos --version 
```

### Using `curl`
```
curl -s --header "Authorization: token=<token>" http://<master-hostname-or-ip>/dcos-metadata/dcos-version.json
```

```
curl -s --header "Authorization: token=$(dcos config show core.dcos_acs_token)" $(dcos config show core.dcos_url)/dcos-metadata/dcos-version.json
```
