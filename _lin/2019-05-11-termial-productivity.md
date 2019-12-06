---
title: Improving productivity on terminal
tags: terminal productivity
---

### Preferred termial: `xfce4-terminal`
I moved from `xterm` to  `xfce4-terminal` due to its ability to resize the font on the fly using `Ctrl Shift +/-`. `xterm` lacked many features which I wanted to use while keeping it lightweight. I have modified some aspects of it though.

* `xfce4-terminal` provides an option which changes the background color automatically of each terminal window. What's better, it chooses colors from a set of dark and light colors depending on your current terminal colorscheme.
* I use `~/.bashrc` to colorcode the prompt to reflect different information such as disk space, tty type etc.
* I modify `~/.inputrc` to use vim keybinding for the terminal. Therefore, in addition to using all basic vim commands, I can press `v` to edit inside a vim instance. Moreover, no need to remember the whole set of editing and movement shortcuts that comes with the terminal.
* I love using the dropdown mode `xfce4-teminal --drop-down`
  
Apart from many shortcuts a linux terminal provides, here are some of my favorite ones.

#### Last command
* In terminal, `!!` means the last command!!!! And `!$` is the argument of the last command.
For example, if `vim /etc/file` gives you permission error, run `sudo !!` which is essentially `sudo vim /etc/file`.
Also, `vim !$` means `vim /etc/file`.
Useful example: `mkdir longdirectoryname`. to enter the directory, do `cd !$`.

* To search for the last command with `cat` in it from the history, do
`!cat:p`.
* To run the last command with       `cat` in it ffom the history, do `!cat`.
* To find commands in the history and run a desired one, do `history | grep cat` and say the command number 455 is the right one that you want to run. Do `!455`.

#### Array approach for typing less:
instead of `cp /etc/file /etc/file-old`, do `cp /etc/file{,-old}`
or, instead of `mv /etc/file.txt /etc/file.pdf` fo ` mv /etc/file.{txt,pdf}`
So, empty field inside `{.,.}` means itself.


Of course, you can define your own `alias` in `.bashrc`, but these shortcuts will save you a lot of typing effot.
[Lifehacker](https://lifehacker.com/5743814/become-a-command-line-ninja-with-these-time-saving-shortcuts) has a few more tips.
