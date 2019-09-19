---
title: wpa_supplicant
---

The best command-line utility so far to connect to wifi.

* Find the network by scanning
```
  iwlist wlp6s0b1 scan | grep ESSID
```
 (The list is NOT ordered according to signal strength.)
 or, use `wifi-menu` but cancel it after it finds the ssids.
 
* To create a config file, see manpage of `wpa_supplicant.conf`
 
 Works only for home wifi (have to check for work wifi): If you do not want to store the password and create a config file, use `wpa_passphrase`
```
 wpa_passphrase ssid_name
```
 You will have to enter the passphrase from stdin and will be encrypted.
 Now copy the code from the file and create a config file. Delete the commented line containing the actual password.

 Alternatively, you can do the following:

 For home wifi, this works:
```
 network={
               ssid="home"
               psk="passphrase"
          }
```
 For GWireless, this works:
```
 network={
        ssid="GWireless"
	key_mgmt=WPA-EAP
	eap=PEAP
	identity="netID"
        password="password"
 }
``` 
 For eduroam, this works:
```
 network={
         ssid="eduroam"
 	key_mgmt=WPA-EAP
 	eap=PEAP
 	identity="email id"
 	password="password"
 }
``` 
 To run the config file with debugging:
``` 
 wpa_supplicant -i wlp6s0b1 -c /path/of/config/file.conf -d
``` 
 To run it in the background, replace `-d` by `-B`
 
 Finally, run dhcpcd if not running  already by dhcpcd or `systemctl restart/start/enable dhcpcd.service`
