---
title: Take screenshots (print screen) in Linux using imagemagick
tags: utility screenshot
---

If you have `imagemagick` installed (which you should), you can do many magical
things with images. Check out the [main website](https://imagemagick.org/) and familiarize yourself with utilities that come with it (e.g. `resize`, `convert` etc.).

The command ```import filename.png```
 gives you a mouse pointer to click on the desired window to take a picture to `filename.png`.
 
 To capture the entire screen, do
 
 ```import -window root filename.png```
 
 We can set up an automatic timestamp in the filenames so that they do not get overwritten (provided you take not more than one picture every second):
 
 ```import -verbose -window root capture-$(date +%d-%h-%Y-%H-%M-%S).png```
 
 In this case,
 
 ```sleep 5; import -window root file.png;```
 
 will be more effective.
 
Taking a screenshot of screen 0 (of `DISPLAY` 0)through some shell: If you log in through `ssh` and want to capture a screenshot at that moment, issue:
 
 ```import -window root -display :0.0 -screen capture-$(date +%d-%h-%Y-%H-%M-%S).png```

