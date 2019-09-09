Manually-download-Flash-Videos
---
title: "Manually download Flash Videos
---
 
 (i)   Visit the YouTube video and wait for it to be downloaded fully.
     Then, run from the command line the command "lsof -n | grep Flash" which shows the files (even memory files!), and filters to those that have Flash in their name.
     You get something like "plugin-co 2461 user 17u REG 8,5 1693301 524370 /tmp/FlashXXVkHEM6 (deleted)".
 
     In Linux, if a file is deleted, it is actually gone only when all programs that opened it earlier are closed. That is, the Flash plugin is using a trick to hide the /tmp/FlashXXVkHEM6 file. It creates it and immediately deletes it. But since the Flash plugin keeps running, it can apparently still use it.
 
 (ii)   From the above line we note the number 2461, which is the process ID. In your case it will be probably different. Then, run "cd /proc/2461/fd" and finally execute "ls -l". This will show you the memory files, and specifically "lrwx------ 1 user user 64 2011-09-16 10:23 17 -> /tmp/FlashXXVkHEM6 (deleted)". The number 17 (in my case) is the filename you can use to access the deleted /tmp/FlashXXVkHEM6. Therefore, simply run "cp 17 /tmp/myyoutubevideo.flv" and you restore the Youtube Video!
