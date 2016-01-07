`sudo dnf update`

`sudo dnf install -y gnome-tweak-tool dconf-editor`

`sudo dnf -y groupinstall "C Development Tools and Libraries"`

`sudo dnf install -y git kernel-devel-$(uname -r)`

```
sudo dnf install --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

`sudo dnf install -y vagrant docker VirtualBox`

`sudo dnf install -y vlc vim`

`sudo dnf install -y --nogpgcheck https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm`

`sudo dnf install -y vim`


```
sudo rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
sudo dnf install -y flash-plugin
```
