`sudo dnf update`


`sudo dnf -y groupinstall "C Development Tools and Libraries"`

`sudo dnf install -y git vim kernel-devel-$(uname -r)`

```
sudo dnf install --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

`sudo dnf install -y vagrant docker VirtualBox`

`sudo dnf install -y terminator vlc`

`sudo dnf install -y --nogpgcheck https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm`

`sudo  dnf install -y https://downloads.slack-edge.com/linux_releases/slack-2.1.2-0.1.fc21.x86_64.rpm`


```
cd /tmp
git clone http://github.com/gabrielelana/awesome-terminal-fonts
cd awesome-terminal-fonts
git checkout patching-strategy
sudo mkdir -p /usr/share/fonts/awesome-terminal-fonts
sudo cp patched/*.ttf /usr/share/fonts/awesome-terminal-fonts
sudo fc-cache -fv /usr/share/fonts/awesome-terminal-fonts
```

`git clone https://github.com/arialdomartini/oh-my-git.git ~/.oh-my-git && echo source ~/.oh-my-git/prompt.sh >> ~/.bashrc`



`sudo dnf install -y gnome-tweak-tool dconf-editor`
