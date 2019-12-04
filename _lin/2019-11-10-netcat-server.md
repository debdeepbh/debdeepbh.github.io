---
title: Simple chat server and client with netcat
tags: server netcat chat utility
---

The [GNU Netcat](http://netcat.sourceforge.net/) is TCP/IP based networking utility.
If you do not have `netcat` installed, install it first. On Arch, you must install `openbsd-netcat`. I accidentally installed the `gnu-netcat` and it did not support many of the commands and the standard examples from the internet failed. Ubuntu already has `netcat` installed.

After installation, use it using `nc`.

1. Open a listening port in the server: ( `-l` for listen, `-v` for verbose)
```
nc -l -v 1432
```

1. Connect to the server:
```
nc server_name_or_ip 1432
```

If it succeeds, cursors on both of the computers will wait. Now type text in one terminal to send it to the other. Congratulations, you have a highly insecure client-server setup running.
