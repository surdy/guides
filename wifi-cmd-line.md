##How To connect to wifi from command line

Find out list of devices using

`ip link`

Suppose name of the interface is `wlp3s0`, you can bring it up by

`ip link set wlp3s0 up`

Then scan the list of available networks using 

`iwlist scan`

Note the `ssid` of the network you want to connect to and configure your setting in `/etc/wpa_suplicant/wpa_supplicant.conf`

```
network={
                 ssid="ssid of the network"
                 psk="passphrase"
                 priority=1
        }
```

Connect to the network using

`wpa_supplicant -B -i wlp3s0 -c /etc/wpa_spplicant/wpa_supplicant.conf`

Run the DHCP deamon
`dhcpcd wlp3s0`
