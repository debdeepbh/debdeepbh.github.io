---
title: Vim shortcuts you should be using
tags: vim productivity shortcut
---

### Touch typing
* `Esc` key with the pinky finger
* `Backspace` with pinky finger as well
* braces and brackets with pinky finger as well

### Shortcuts available by default
* `S` (substitute) deletes the current sentence and goes into the edit (compared to `DD` where the current line vanishes)
* `:set textwidth=69` and `:set colorcolumn=+1` breaks the line after 69 characters. (`linebreak` makes sure that that words do not break in the middle). However, after editing for a while in this mode, lines will have different width. It can be fixed with `gq` command: `gqap` (here, `ap` is _a paragraph_)
* Also, `s` is a better alternative to `r` to edit strings
* `W`, `E`, `B` instead of `w`,`e`,`b` to avoid special characters. Therefore, `dW`, `dE`, `dB` etc
* `Crtrl+E/Y` to  move page without moving the cursor so that I don't have to look at the bottom of the screen all the time; Even better: zz adjust the screen  so that the cursor is at the middle of the screen. `zb` and `zt` to place it in the top and bottom.
* `tx` to jump till the next occurrence of character `x` -- instead of `fx` which brings the cursor on the character. So, use `dtx` instead of `dfx` to delete till the character `x`, instead of including the character `x`. Useful for deleting till the next parenthesis with `dt)`.
* Once `f` or `F` or `t` or `T` is pressed followed by a character, pressing `;` and `,` will take the cursor to match the same character further in that direction. Use `#` and `*` for the occurrence of the same word under the cursor.
* `gf` and `gx` to open the file or hyperlink under the cursor. `gf` on a hyperlink will  open the html file for editing while `gx` will launch it in the browser.
* `g;` and `g,` to move through the changelist
* `ddp` to switch current line with the next, like `xp`
* `C` or `D` - change or delete the rest of the line
* `U/u` on a visual selection to make all uppercase/loswercase and `~` to flip the case
* `=` to fix indentation of code like this: `==` to fix the correct line, `=5j` to fix the next 5 lines, place cursor on an opening brace `{` and press `=%` to fix until the matching closing brace i.e. the whole block. Finally, if the cursor is inside a code block  of `{.}`, pressing `=a{` will fix the indentation of the whole block
* `Ctrl+w` to delete word back in insert mode. In fact, I have also mapped `Ctrl+Backspace` to the same to be consistent with browser editing. However, this does not work on terminal though.
* `Ctrl+a` to insert string inserted in last edit mode, while being inside the insert mode. Pressing `.` does the same in edit mode.
* `:set ic` to set ignorecase and `:set noic` to bring back case while searching
* `"` to jump to the place last exited buffer, `` ` `` to jump back to where you jumped from, `` `[ `` or `` `] `` to the start or end of last yanked or changed buffer,  `` `< `` or `` `> `` to the start or end of the last visual selection.
* `:reg` to see all the registers, `:reg p q r` to see only those registers, registers `0-9` fills up with deleted lines.
* `"rY` yank current line to the buffer `"r`, use `"rp` to paste the content of buffer `"r`. In insert mode type `Ctrl+r` then `s` to paste the content of buffer `s`.
* `"=` can do integer calculations of evaluate commands like `system('ls')` and can be used via `Ctrl+r=` or `"=p` 
* Buffers `"%` is the current filename and `":` is the most recently executed vim command
* First type up a macro then execute it as a string: yank the macros string to a buffer (say `m`) then type `@m` to execute it. In fact, when you record a macro (with `q`), it gets copied to the buffer of the same name.
* `:ab <abbreviation> <full\ name>` will expand abbreviation while typing, use `:una <abbreviation>` to remove the rule.
* `Ctrl+A`, `Ctrl+X` to increment or decrement the first number found after the cursor
* `g Ctrl+g` to get work/line/char count and just `ctrl+g` to show the file info (also `:%`) and number of lines etc. 
* `g-` or `:earlier` to return the buffer to the earlier state, like undo `u` but does not erase the other undo branch. Similarly `g+` and `:later`. Finally `:earlier 1m` or `1h` or `5f` (`f` for number of save times ago)
* matching or unmatched braces: `[[` to jump to the previous opening brace. Similarly `]]`. Also, `[{`, `[(` will take you to the previous unmatched opening brace and parenthesis. Similarly for `[}` and `[)`.
* Create a new line and go to insert mode after and before the cursor with `o` and `O`. To do the same without going into insert mode: mapped `oo` and `OO` for that reason, but this also makes `o` and `O` very slow
* Delete backward when the cursor is on the last letter of the word (`dB` does not work): done with `dge` and `dgE`
* Copy-pasting between firefox and terminal: done with `clipboard=unnamedplus` in your `vimrc` 
* Navigating a multi-line sentence with `gj` `gk`
