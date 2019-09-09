---
title: "Enable Visual Effects"
---
 
 * Enable Wobbly Windows
 * Enable Shift Switcher (Cover) and Change Shortcut to <Ctrl>+<Tab> for next window and <Ctrl>+<Shift>+<Tab> for previous window.
 
5. Installing sound driver:
 
 * In terminal, write: sudo gedit /etc/modprobe.d/alsa-base.conf
 * In the end of the file, add this line: options snd-hda-intel model=6stack-dell (For that dell studio 1435)
 options snd-hda-intel model=ideapad (For lenovo ideapad Z560)
 * Save the file and Reboot.
 * Open pulse audio and enjoy full features.
