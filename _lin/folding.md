---
title: "Using file and folding"
---

Maintained using indentation folding and searched using the headings.
Settings have to be applied to this file only using vim -S TODOsettings.vim

## Folding Help:
 
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
  
 Folding Options (Should change in TODOsettings.vim file to make it permanent.)
set foldnestmax=10      | "deepest fold is 10 levels
set nofoldenable        | "dont fold by default
set foldlevel=1         | "this is just what i use
set shiftwidth=1 	| "to consider spaces as one foldlevel away
 
## Searching Help:
 ** :set foldopen-=search  		to stop folds from opening on search, which is even better.
    :folddoopen s/old/new/ge 	to replace old with new in the lines which are not folded. 

## Warning: 
 Smartindent is on, hence use <F2> before pasting into it.
 
## Want: 
 Not more than 2 stages of folding
 Search within the visible folded text
 Search within the invisible text inside folds
 INdent = on
