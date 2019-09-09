---
title: "Create a startup script to mount Hard disk drives"
--- 

  * Goto /media/ and create 3 directories called "windows", "disk3", storage".
 	cd /media/
 	sudo mkdir windows disk3 storage
  * Create a file named "mounting" with following content:
 
 ##startup script to mount the disk drives
 sudo mount /dev/sda1 /media/windows
 sudo mount /dev/sda3 /media/disk3
 sudo mount /dev/sda5 /media/storage
 #EOF
 
  * Change file permission to +x:
 	chmod +x mounting
  * Copy the file to /etc/init.d/:
 	sudo cp mounting /etc/init.d/
  * Update:
 	sudo update-rc.d mounting defaults
