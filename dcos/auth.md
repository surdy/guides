## How to authenticate with the cluster using curl ?

```
curl -X POST -H 'Content-type: application/json' -d '{"uid":"adminuser", "password":"somepassword"}' http://<dcos_url>/acs/api/v1/auth/login
```

returns 

```
{"token": "sometoken"}
```

Then you can use the token for auth 

```
curl -X GET --header "Authorization: token=sometoken" http://<docs_url>/marathon/v2/apps
```


### Alt

```
LOGIN_TOKEN=`curl --data '{"uid":"admin", "password":"admin"}' --header "Content-Type:application/json" http://<dcos_url>/acs/api/v1/auth/login | jq -r .token`
```

```
curl -k -H "Authorization: token=$LOGIN_TOKEN" http://<dcos_url>/mesos/master/state-summary
```
