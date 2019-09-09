---
title: Unity 3D
---
 Install linpng12 from AUR.
 
 Install unity 3d from AUR. Note: The package build is 11GB  after makepkg -s and creates a .sh file and a directory. Instead of pacman -U, use the generated install script as there will be no .xi file to install. This is also an advantage since these files can be moved to another partition and launched. These are 3GB long.
 
 Watched tutorial on game rolling the ball on their official site.
 Lessons:
 A "is Trigger" object with a "Rigid body" component is a "Dynamic collider" and uses more resources.
 A "is Trigger" object without"Rigid body" component is a "Static  collider" is ideal. Setting "kinemetic" field will give you desired result.
 
106. Progress bar for cp, firefox download, dd, tar, cat
 Use 'progress'.  https://github.com/Xfennec/progress
 See man page for details.
 
107. wpa_supplicant
 Find the network by scanning
  iwlist wlp6s0b1 scan | grep ESSID
 The list is NOT ordered according to signal strength.
 or, use wifi-menu but cancel it after it finds the ssids.
 
 To create a config file, see manpage of wpa_supplicant.conf
 
 Works only for home wifi (have to check for work wifi): If you do not want to store the password and create a config file, use wpa_passphrase
 wpa_passphrase ssid_name
 you shall enter the passphrase from stdin and will be encrypted.
 Now copy the code from the file and create a config file. Delete the commented line containing the actual password.

 Alternatively, you can do the following:

 For home wifi, this works:
 network={
               ssid="home"
               psk="passphrase"
          }

 For GWireless, this works:
 network={
        ssid="GWireless"
	key_mgmt=WPA-EAP
	eap=PEAP
	identity="netID"
        password="password"
 }
 
 For eduroam, this works:
 network={
         ssid="eduroam"
 	key_mgmt=WPA-EAP
 	eap=PEAP
 	identity="email id"
 	password="password"
 }
 
 To run the config file with debugging:
 
 wpa_supplicant -i wlp6s0b1 -c /path/of/config/file.conf -d
 
 To run it in the background, replace -d by -B
 
 Finally, run dhcpcd if not running  already by dhcpcd or systemctl restart/start/enable dhcpcd.service
 
108. Find out name of the linux distribution
 cat /etc/*-release
 typically, os-release has all the info, including the pretty name.
 For the linux kernel version, cat /proc/version
109. Determine which physical disk partition mounted on a directory
 For example, the / filesystem is installed on
  df /
 The directory /root is located in
  df /root
 Conversely, to see a list of all block devices and their mountpoints,
  lsblk
 
