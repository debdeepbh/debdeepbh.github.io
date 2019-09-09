---
title: "Peforming xserver activities through tty or remote ssh shells"
---
 
 After logging in, set the DISPLAY variable to :0.0 or to :0 or any other if necessary (which can be found by issuing w command and looking at the "from" field)
 
 export DISPLAY=:0.0
 
 Then  issue your commands like you do in the terminal.
 
 Note: apparently you cannot run a gui program in other user's tty even by setting the DISPLAY to the user's tty.
 
15. Simple GTK pop-ups:
 
 First export DISPLAY 
 There is a software called zenity that'll do your work. See zenity --help for more options. Example:
 
 zenity --info --text "hello there!"
