---
title: "Setting up raspberry pi zero w"
---

### Ethernet over usb:
Follow the popular guide to add two lines related to modules in the first (boot) partition:

1. open up the boot partition on the micro sd with finder and in the file `config.txt` add `dtoverlay=dwc2` to a line on the bottom and save it.
2. Create a new file called ssh using textedit and save it onto the boot partition. Use 'get info' to remove the extension on the file, and it should appear as an EXEC file. You can now eject the card and boot it on your RPi
3. Finally, open up the cmdline.txt. replace all text with this:
```
dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait modules-load=dwc2,g_ether quiet init=/usr/lib/raspi-config/init_resize.sh 
```

4. Edit `/etc/network/interfaces` to add usb0 related info:
```
allow-hotplug usb0
iface usb0 inet dhcp 
```

5. Plug in a *good* usb cable to the usb port, not the power in and then set up the retrying nm-applet attempt to connect to the wired network and fail repeatedly. At this point, you can connect to the pi using `ssh pi@raspberrypi.local`
If the repeated attempt to connect and fail message from `nm-applet` is bothersome, run `dhcpcd enp7e0u1i7` (or whatever is the hardware name from `ifconfig`) on your laptop. Note: `dhcpcd` in not installed by default so install it using `sudo apt-get install dhcpcd5`

6. For wifi:
Use `wpa_passphrase <ssid_name>`  to get the config file. Add it to `/etc/wpa_supplicant/wpa_supplicant.conf`
Next, add the following to `/etc/network/interfaces`
```
auto wlan0
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

You can set up multiple networks in the `wpa_supplicant.conf` file and the first available one will be used (I think. Or, maybe w.r.t. signal strength? However, it is working according to order of appearance)
