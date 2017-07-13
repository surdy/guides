```
curl -H "Authorization:curl --header token=<token>" -H "Accept: application/vnd.dcos.package.install-response+json;charset=utf-8;version=v1" -H "Content-type: application/vnd.dcos.package.install-request+json;charset=utf-8;version=v1" -X POST -d '{"packageName": "chronos", "packageVersion": "2.4.0", "options": {}}' <dcos_url>/package/install
```

```
curl -H "Authorization:curl --header token=<token>" -H "Accept: application/vnd.dcos.capabilities+json;charset=utf-8;version=v1" <dcos_url>/capabilities
```
