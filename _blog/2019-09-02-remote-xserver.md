---
title: Performing xserver activities through tty or remote ssh shells
tags: xserver remote ssh 
---
If you have an Xserver running in a remove computer, you can perform GUI related actions via ssh.
 
 After logging in, set the `DISPLAY` variable to `:0.0` or to `:0` or any other if necessary (which can be found by issuing `w` command and looking at the `from` field).

Export the display as an environment variable using:
``` 
 export DISPLAY=:0.0
```
 Then  issue your GUI commands like you do in the terminal.
 
**Note:** apparently you cannot run a gui program in other user's tty even by setting the `DISPLAY` to the user's tty.
 
***

### Simple GTK pop-ups:
 
 First export `DISPLAY` as above.
 There is a software called `zenity` that'll do your work. See `zenity --help` for more options. Example:
``` 
 zenity --info --text "hello there!"
```

### Launching remote GUI elements locally

While loggin in via ssh, use `-X` to allow the local Xserver to display the output of the remote Xserver. e.g.
```
ssh -X user@remote-host:~/
firefox
```

