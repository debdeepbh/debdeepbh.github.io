---
title: Installing and using Cocalc notebook locally
tags: cocalc sage language math
---
[CoCalc](https://cocalc.com/) is probably the best outcome of collaborative opn source efforts as of today. It is a collaborative online computing environment, mostly for [Sage](http://www.sagemath.org/) (an open source mathematical software). Apart from sage worksheets, it allows octave, jupyter notebooks, latex and R document editing, and many more. You can just create an account in their website and start using right away.

But the best part is that you can install Cocalc as a server and let others log in to it and collaborate. No need to install `sage` or `sagemath`.

Follow the instruction to install the [`cocalc-docker`](https://github.com/sagemathinc/cocalc-docker). It is just one
line long code. It will download,
extract and install. I had to use sudo to get it to work since I
installed docker using sudo (`sudo apt-get install docker.io`). 
To open it in browser, make sure to use `https://localhost` instead of
`http://localhost`.

I had create account (fake email ids are ok, since they are local)

To start and stop `cocalc`, use 

```
sudo docker start cocalc
```

and 

```
sudo docker stop cocalc
```

### Usage:
* To view equations in latex rendering, use the function `view()`. To
print out the latex code of it, use the function `latex()`.
* To turn the latex rendering on by default, you can use `%typeset_mode` to `True` at the beginning of the sheet

* To define variables in a latex-friendly way so that the view command
prints it right, use

```
u_th_x = var('u_th_x', latex_name = 'u_{\\theta}(x)'}
```

Later, do `view(u_th_x)` to see it rendered correctly.

