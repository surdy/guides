# Create a single systemd service docker image

These intructions are based on Fedora 23 but can be adapted to any other distro.

## Creating the base systemd image

We would like to have multiple such single service docker images, so lets first create a base systemd image.  

To inform systemd that it is running within a container we need to set the `container` environment variable to `docker`.  

We should make sure the image is up to date by running a `dnf update` and then cleanup the cache for this image layer. `deltarpm=false` is there to supress some warnings [details here](https://fedorahosted.org/spin-kickstarts/ticket/56)

We would need to remove unit file links from `/lib/systemd/system/*wants/` and  `/etc/systemd/system/*wants/`. Removing these links would get us a systemd container image that would only run systemd and journald.

Finally we need to tell the image it requires the `/sys/fs/cgroup` volume mounted into it and execute the `init` command.

Here is the Dockerfile that does all of the above:

```
FROM fedora:23
ENV container docker
RUN dnf -y --setopt=deltarpm=false update; dnf clean all
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
```

Lets build the docker image.
```
docker build -t systemd_fedora .
```

Now we have a base systemd docker image we can use for creating single service images.


## Creating the signle service image

In this example we will be creating a nginx image using the base systemd image we just created.

All we need to do here is start from the base image and install the nginx service and enable it.

Since nginx binds to port 80, we need to specify this in the image.  

Finally since systemd will be managing the service within the container we specify `/usr/sbin/init` as the command to run within the container.

Here is the docker file:
```
FROM systemd_fedora
RUN dnf -y install nginx; dnf clean all; systemctl enable nginx.service
EXPOSE 80
CMD ["/usr/sbin/init"]
```

Lets build the nginx image:
```
docker build -t nginx_fedora .
```


The container needs to be run in priviledged mode because systemd requires the `CAP_SYS_ADMIN` capability. systemd the cgroup file system within the container, so the cgroup file system `/sys/fs/cgroup` needs to be mounted to the container using the volume mount

```
sudo docker run --privileged -ti -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 nginx_fedora
```
