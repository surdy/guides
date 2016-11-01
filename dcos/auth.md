## How to authenticate with the cluster using curl ?

`curl -X POST -H 'Content-type: application/json' -d '{"uid":"adminuser", "password":"somepassword"}' http://your.master/acs/api/v1/auth/login`

returns `{"token": "sometoken"}`

`curl -X GET --header "Authorization: token=sometoken" http://<host-name>/marathon/v2/apps`
