---
title: "IP and hostname resolution"
---
 
* List hostnames and ips:
```
 arp -a
```
or
```
 avahi-browse -a
```
* For IP <---> Hostname, use resolveip: 
```
 resolveip IP/Hostname
```
 
* Sometimes, one way: IP --> Host: 
```
 host ip_address
```
 but most of the time this fails due to the DNS server, I think.
* For IP <--- Host, nslookup:
```
 nslookup host
```
 This also does not work for internal hosts.
