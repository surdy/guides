## How to get build information for various components of DC/OS ? 

## From the node
```
cat /opt/mesosphere/active.buildinfo.full.json 
```

## Using curl
```
curl -s --header "Authorization: token=<token>" http://<master-host-name>/pkgpanda/active.buildinfo.full.json
```

```
curl -s --header "Authorization: token=$(dcos config show core.dcos_acs_token)" $(dcos config show core.dcos_url)/dcos-metadata/dcos-version.json
```
