---
title:  Detect live ports using nmap
---
 
 Know the live ports of your OWN hosts, and the connected ips:
```
 sudo netstat -tpan
```
 
 Know if a particular port is open or not in a remote host:
```
 nmap -p port host/ip
```
Moreover, 
```
 nmap --script=smb-enum-users 192.168.2.167 -p 445|perl -le 'while(<STDIN>){if(/^.*?\\(\w+)\s+.*/) { print "$1"; }}'
```
