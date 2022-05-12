---
title: Handy pdf editing tools
tags: pdf utility merge pdftk
---
The filetype I handle most frequently is pdf. Here is a list of my most frequently used pdf-related actions. 

* Converting pdf to png:
```
pdftoppm -png input.pdf output
```

`pdftk` is another brilliant tool to operate on pdf file. The main thing to remember is `cat output`.

* Merging pdf files:
```
pdftk file1.pdf file2.pdf cat output outputfile.pdf
```


* Extract page 2-6 from a pdf:
```
pdftk file.pdf cat 2-6 output outputfile.pdf
```

* Drop page 13 from a pdf:
```
pdftk file.pdf cat 1-12 13-end output outputfile.pdf
```

You can also use `pdftk` to encrypt pdf files. See `man pdftk`. It's amazing.

