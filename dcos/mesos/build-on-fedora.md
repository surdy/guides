## Install a few utility tools
`sudo dnf install -y tar wget git`

## Fetch the Apache Maven repo file.
`sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo`
`sudo sed -i -e 's/epel-$releasever/fedora-23/' /etc/yum.repos.d/epel-apache-maven.repo

## Install essential development tools.
`sudo dnf groupinstall -y "Development Tools"`

## Install other Mesos dependencies.
`sudo dnf install -y apache-maven python-devel java-1.8.0-openjdk-devel zlib-devel libcurl-devel openssl-devel cyrus-sasl-devel cyrus-sasl-md5 apr-devel subversion-devel apr-util-devel`

## Change working directory.
`cd mesos`

## Bootstrap (Only required if building from git repository).
`./bootstrap`

# Configure and build.

```
mkdir build
cd build
../configure
make
```
