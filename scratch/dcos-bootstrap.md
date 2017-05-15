```
cat > Dockerfile << EOF
FROM docker:dind

RUN apk add --no-cache \
                bash \
                tar \
                sed
EOF
```

`sudo docker build -t dcos-bootstrap .`

`mkdir genconf`

```
cat > genconf/ip-detect << EOF
#!/bin/sh
# Example ip-detect script using an external authority
# Uses the AWS Metadata Service to get the node's internal
# ipv4 address
curl -fsSL http://169.254.169.254/latest/meta-data/local-ipv4
EOF
```

```
cat > genconf/config.yaml << EOF
---
bootstrap_url: http://5.6.7.8:8080
cluster_name: '<cluster-name>'
exhibitor_storage_backend: static
ip_detect_filename: /genconf/ip-detect
master_discovery: static
master_list:
- 1.2.3.4
resolvers:
- 8.8.4.4
- 8.8.8.8
EOF
```

`docker run --privileged -v $PWD/genconf:/genconf -d dcos-bootstrap`

`docker exec -it <image-id> /bin/bash`

`curl -O https://downloads.dcos.io/dcos/stable/commit/0ce03387884523f02624d3fb56c7fbe2e06e181b/dcos_generate_config.sh`

`bash dcos_generate_config.sh`
