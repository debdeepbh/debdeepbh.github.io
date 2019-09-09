---
title: "Compress and uncompress (zip/unzip) files using aunpack"
---
 To extract all files from archive `foobar.tar.gz' to  a  subdirectory  (or the current directory if it only contains one file):
  aunpack foobar.tar.gz
 
 To create a zip archive of two files `foo' and `bar':
  apack myarchive.zip foo bar
 To compress the content of current directory into a zip file called comp.zip
  apack comp.zip *
 
 To list contents of the rar archive `stuff.rar':
  als stuff.rar
114. calendar.vim
 Since  I have pathogen to install vim plugins, cloning the repo to .vim/bundle/ installs it.
 Setting the google options in .vimrc, when I do :Ca inside vim, I cannot copy the link got google authentication. So I opened it in gvim and copied it. But in gvim, I cannot paste the code that I received from google. So I hand-typed it. Very annoying.

 Here is a quick possible solution:
 1. Open gvim
 2. Type :Ca
 3. Copy the link
 4. Paste in browser, proceed, get a code
 5. Edit the file .vim/bundle/calendar.vim/google/client.vim and navigate to the line: 
 let code = input(printf(calendar#message#get('access_url_input_code'),
 (This line is inside a function called access_token_async. The input code here is not able to access the bufferes "+, "* etc. So we manually supply the value of variable 'code'. Make sure this modification does not stay for long)
 6. Modify the line to
 let code = 'xxxx_your_code_goes_here_xxxx'
 7. Save the file.
 8. Open usual vim and run :Ca and it should work directly.
 9. Undo the changes in client.vim and save it back. This step is necessary because you don't want to leave the code in a config file that is possibly uploaded to github. Make sure there are no git commits in the time interval between the two saves otherwise someone can look at the history of the file and retrieve it.
 
 See the calendar.vim/doc/calendar.txt for a complete help which I followed mostly.
 As a shortcut in awesomerc, add `xterm -e vim +:Ca` to open vim in a terminal with command :Ca and mapped it to Modkey+C
 
  

