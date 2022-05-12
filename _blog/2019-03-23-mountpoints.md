---
title: Moving directories to their own partitions
tags: mount partition fstab
---
After using a Linux for a while, if you may realize that your `/root` or `/home` partition needs more space than anticipated. So, it might be useful to move these directories to their own partitions, if you haven't done so originally. This setup also has the advantage that you can format and install a new copy of Linux without losing the user data. Here is how to move `/root` to its own partition.

* Create new ext4 partition, say `/dev/sda7`. Mount it in a directory, say `/otherlin`
* Copy all data from `/root` to `/otherlin` using the following commands
```
  cp -urp /root/. /otherlin/
```
* Note that `-r` for recursive copy and `-p` is to preserve permission, date etc.
 Here, `-u` means update, i.e. doesn't overwrite already copied files. 
  Note that, `cp -rp ~/* /otherlin`
  	is not enough since it does not copy the dot files.
 Alternative tools suggested: `rsync`, and `curl` (nice use!) to have a progress bar etc.
* Find the UUID for the new partition using
`bkid`
* Edit `/etc/fstab` and add the line
```
  UUID=daef66f2-4c7a-4daa-9d7d-f217a3a3994f	/root         	ext4      	rw,relatime,data=ordered	0 2
```
 Here, the UUIS should be replaced by the appropriate one.
 0 means it doesn't have to be backed up. 2 means the system checks the partition after the first one (1 is `/` so `/` gets checked first; 0 means no checking).

* Back up the current /root by 
```
  mv /root /root.old
```
 It failed the first time and had to uncomment the new line in fstab and reboot and try again to succeed.
* Remount all the drives by
```
 mount -a
```

