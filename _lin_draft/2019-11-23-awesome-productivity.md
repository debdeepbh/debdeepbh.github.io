---
title: Productivity shortcuts for awesome window manager
tags: awesome wm productivity lua
---


Awesomewm related shortcuts:

modkey + j/k/h/l = browse by direction
altkey + j/k = browse by order
modkey + d = dmenu
modkey + s = show help (not so helpful)

Layout manipulation:

modkey + shift + j/k = swap with the next client by index
modkey + F2 = rename current tag

modkey + shift + h/l = increase/decrease number of master clients
modkey + ctrl  + h/l = increase/decrease number of columns
modkey + shift + enter = move to master

The slight issue is: when you do modkey + ctrl + enter to set a client as master, it replaces the first client already set as master. So, if you want to add some client as master, first, move the topmost master client down using modkey + shift + j and then navigate to the client you intend to make master and then hit modkey + ctrl + enter. Downside is: the second master client is not master anymore :( Not sure if there is any shortcut for this.
Alternatively, move the slave client up until it is the first slave client. Then use Modkey + shift + h to increase the number of master client and automatically the fist slave client will be move to be the last master client.

modkey + u = jump to the urgent client (what is urgent client?)

These two are new and should be used:
modkey + tab = jump back to the previous client
modkey + Esc = jump back to the previous taglist

altkey + shift + l/h = increase/decrease master width


modkey + ctrl + space = toggle floating
modkey + t = keep on top

modkey + shift + number = move the focused client to taglist number
modkey + ctrl + shift + number = copy focussed client to taglist number, toggle

Added myself: 
modkey + shift + n = create a new tag
modkey + shift + d = delete a tag
modkey + F2 = rename a tag


TODO:
Find out how to restart xinput without restarting, possibly via modprobe.
