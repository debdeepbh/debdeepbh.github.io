---
title:  Live ports
---
 
 Know the live ports of your OWN hosts, and the connected ips:
 sudo netstat -tpan
 
 Know if a particluar port is open or not in a remote host:
 nmap -p port host/ip
 
 nmap --script=smb-enum-users 192.168.2.167 -p 445|perl -le 'while(<STDIN>){if(/^.*?\\(\w+)\s+.*/) { print "$1"; }}'
