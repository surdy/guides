`sudo yum -y install yum-plugin-fastestmirror yum-cron`

`sudo yum -y update`

`sudo yum -y install gnome-tweak-tool dconf-editor`

`sudo yum -y groupinstall "C Development Tools and Libraries"`

`sudo yum -y git kernel-devel ruby ruby-devel`

`sudo vagrant chef docker VirtualBox`

```
sudo yum -y localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

`sudo yum install vlc`

```
sudo rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
sudo yum install flash-plugin
```

`sudo yum localinstall --nogpgcheck https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm`
