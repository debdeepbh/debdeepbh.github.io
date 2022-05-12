---
title: Handling compressed files without remembering the parameters
tags: zip unzip compress extract utility
---
Often times, you might be asking yourself, what are the parameters for extracting a `tar` file? (answer: `-xvf`) In any case, to avoid memorizing individual parameters for zip, tar, rar etc, use `atool`.

* Install `atool` using `apt-get`: `sudo apt-get install atool`.
Commands like `apack`, `aunpack`, `acat` from `atool` are now at your disposal.
 
* To extract all files from archive `foobar.tar.gz` to  a  subdirectory  (or the current directory if it only contains one file):
 ```
aunpack foobar.tar.gz
```
 * To create a zip archive of two files `foo` and `bar`:
```
apack myarchive.zip foo bar
```  
 * To compress the content of current directory into a zip file called `comp.zip`:
```
apack comp.zip *
``` 
 * To list contents of the rar archive `stuff.rar`:
```
als stuff.rar
```
