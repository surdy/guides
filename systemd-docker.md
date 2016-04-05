```
FROM fedora:23
ENV container docker
RUN dnf -y --setopt=deltarpm=false update; dnf clean all
RUN dnf -y install systemd; dnf clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
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

`docker build -t systemd_fedora .`


```
FROM systemd_fedora
RUN dnf -y install nginx; dnf clean all; systemctl enable nginx.service
EXPOSE 80
CMD ["/usr/sbin/init"]
```

`docker build -t nginx_fedora .`

`sudo docker run --privileged -ti -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 nginx_fedora`

