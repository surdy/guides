#Macbook fixes for Fedora (Gnome)

##Wireless card
Install RPM Fusion repos
```
sudo dnf install -y --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

Install the broadcom wireless drivers:
```
sudo dnf install -y kernel-devel-$(uname -r) akmod-wl
```

Reload wireless module
```
# Make sure the module built for your kernel
sudo akmods

# See if the module is loaded (if no results, it's not)
sudo lsmod | grep wl

# Manually load the module
sudo modprobe wl
```

##High DPI fixes
###Firefox fix
Set `layout.css.devPixelsPerPx` to `1.5` or `2`
###Gnome font fix
Install `gnome-tweak-tool` and use it to set the `Sclaing Factor` under the `Fonts` menu to a value of your linking `.75` worked for me

##Things to put in a startup script
###Fix "FPDMA QUEUED" errors
`echo 1 > /sys/block/sda/device/queue_depth`
###Make Function keys default (instead of media keys)
`echo 2 > /sys/module/hid_apple/parameters/fnmode`
###Enable touchpad tap
`synclient TapButton1=1`
###Optimize Power Consumption
```
/usr/libexec/gsd-backlight-helper --set-brightness 4
rfkill block bluetooth
echo 50 > /sys/class/leds/smc::kbd_backlight/brightness
echo '1500' > '/proc/sys/vm/dirty_writeback_centisecs'
echo 'min_power' > '/sys/class/scsi_host/host0/link_power_management_policy'
echo '1' > '/sys/module/snd_hda_intel/parameters/power_save'
echo '0' > '/proc/sys/kernel/nmi_watchdog'
echo 'auto' > '/sys/bus/usb/devices/1-5/power/control'
echo 'auto' > '/sys/bus/usb/devices/1-3.3/power/control'
echo 'auto' > '/sys/bus/usb/devices/2-3/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:03:00.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:00.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:02.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:03.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:14.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1c.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1c.1/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:04:00.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:16.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:02:00.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1f.3/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1f.0/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1c.4/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1c.5/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1c.2/power/control'
echo 'auto' > '/sys/bus/pci/devices/0000:00:1b.0/power/control'
```

##Misc Fixes
###Turn off CPU Turbo mode (so that it does not run too hot)
` su -c "echo -n 1 > /sys/devices/system/cpu/intel_pstate/no_turbo"`
###Fix immediate resume after suspend 
```
su -c "echo XHC1 > /proc/acpi/wakeup"
su -c "echo LID0 > /proc/acpi/wakeup"
```
to toggle the state to `disabled`
