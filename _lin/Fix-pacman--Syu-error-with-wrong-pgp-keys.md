---
title: Fix pacman -Syu error with wrong pgp keys
---
 pacman-key --refresh-keys
 
111. Killing processes
 To find the pid of the process, do
  pidof processname
 or,
  ps aux | grep processname
 To kill process with pid
  kill pid
 To kill stubborn unresponsive process
  kill -9 pid
 To kill all processes with name
  killall processname
  killall -9 processname
  
 Unmounting partitions in use: Find out which process is using it by
  lsof | grep /mountpoint
  killall/kill [-9] processname/pid 
112. [Abandoned: couldn't see any improvement] Speeding up firefox by moving the profile to ram
 https://fixmynix.com/speed-up-firefox-with-ram-cache-and-tmpfs-linux/
 Note: Setting  browser.cache.disk.enable to false and setting browser.cache.memory.enable to true accelerates reloading recently loaded page elements. It comes with the variable browser.cache.memory.capacity which has to be created and specified as well. Eg: 409600. Reference: http://kb.mozillazine.org/Browser.cache.memory.enable
 Note: This specified size is OUTSIDE the profile directory of firefox. The precess so far has not used any ramfs yet.

 N: Didn't follow the first few http, ssl variable modifications. Starts from editing memory_cache variable.
 Main problem: the profile directory gets bigger and bigger and soon the tmpfs is full.
 Q: Can I sync while closing firefox instead of cronjob every 5 mins? Well, to save accidental crash, 5 mins seems better, still.
 Q: How to preserve the installed addons and login to pushbullet?
 Q: Why allocate _capacity 2M and create tmpfs for 128mb?
 Q: Moving .vimrc to ram.
 Q: Wat else can I move to ram?
