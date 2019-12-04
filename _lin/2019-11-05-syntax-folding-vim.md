---
title: Syntax folding in vim and custom folding for a file
tags: vim folding productivity
---
Syntax folding in vim is a powerful feature that makes navigation very easy. Folding can also be used to create an ad-hoc index for the file. Here are my frequently used folding commands.

### Folding Help:

| * | Keyseq | Description
|-----------|---------|---------------
|   | zi |	switch folding on or off
| * | za |	toggle current fold open/closed
|   | zc |	close current fold
| * | zR |	open all folds
| * | zM |	close all folds
|   | zv |	expand folds to reveal cursor
| * | zj,zk | jumps to the next/previous fold, even when unfolded
|   | zo,(zO) | jumpsopen fold (recursively)
|   | zc,(zC) | jumpsclosefold (recursively)
| * | zA	| toggle folds recursively
  
## Creating custom folding options for a file

You can create a vim config file `customfolding.vim` for a particular file and launch the file with `vim -S customfolding.vim`. 

#### Folding Options 

Options in vimrc | Description
--------------|-----------
`set foldnestmax=10`    | "deepest fold is 10 levels
`set nofoldenable`        | "dont fold by default
`set foldlevel=1`         | "this is just what i use
`set shiftwidth=1` 	| "to consider spaces as one foldlevel away

Additionally, you can add the following to the custom vimrc for better searching 

 ```
" DO not expand folds while searching
set foldopen-=search
```

to stop folds from opening on search, which is even better. Moreover, use 
`:folddoopen s/old/new/ge`
 to replace `old` with `new` in the lines which are not folded. 

#### Warning: 
 I keep my `smartindent` on, hence I use `<F2>` before pasting into the file.
 
#### Example:
Here is an example of a vimrc where lines starting with one whitespace will be folded into the preceding line:
```
set smartindent

setlocal foldmethod=expr
setlocal foldexpr=(getline(v:lnum)=~'^$')?-1:((indent(v:lnum)<indent(v:lnum+1))?('>'.indent(v:lnum+1)):indent(v:lnum))
set foldtext=getline(v:foldstart)
set fillchars=fold:\ "(there's a space after that \)
highlight Folded ctermfg=DarkGreen ctermbg=Black

" DO not expand folds while searching
set foldopen-=search 
```
 


