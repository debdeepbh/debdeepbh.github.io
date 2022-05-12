---
title: Create a startup script to mount hard disk drives automatically
tags: mount rc.d
---
If you are using a DIY distribution like Arch, this is a necessary thing to do after every reboot. So, it is better to wrap the steps up in a script and automate it using `rc.d`. Say, I have 3 partitions that I would like to mount to 3 directories.

  * Goto `/media/` and create 3 directories called `windows`, `disk3`, `storage`.
```
cd /media/
sudo mkdir windows disk3 storage
```
  * Create a file named `mounting` with following content:
``` 
 ##startup script to mount the disk drives
 sudo mount /dev/sda1 /media/windows
 sudo mount /dev/sda3 /media/disk3
 sudo mount /dev/sda5 /media/storage
 #EOF
```
 
  * Make the file executable:
 	`chmod +x mounting`
  * Copy the file to `/etc/init.d/`:
 	`sudo cp mounting /etc/init.d/`
  * Update your `rc.d` so that the script is executed at startup:
 	`sudo update-rc.d mounting defaults`

