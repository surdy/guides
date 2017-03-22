  ```
  curl -i \
      -d slaveId=f64307a0-4151-41fe-a50c-206aa181f05c-S1 \
      -H "Authorization:curl token=$(dcos config show core.dcos_acs_token)" \
      -d resources='[
       {
         "name": "cpus",
         "type": "SCALAR",
         "scalar": { "value": 2 },
         "role": "dev",
         "reservation": {
           "principal": "dcos_anonymous"
         }
       },
       {
         "name": "mem",
         "type": "SCALAR",
         "scalar": { "value": 200 },
         "role": "dev",
         "reservation": {
           "principal": "dcos_anonymous"
         }
       },
      {
         "name": "ports",
         "type": "RANGES", 
         "ranges": {"range": [{"begin": 31001, "end": 31100}]},
         "role": "dev",
          "reservation": {
            "principal": "dcos_anonymous"
          }
       }  
     ]' -X POST $(dcos config show core.dcos_url)/mesos/master/reserve 
     ```
