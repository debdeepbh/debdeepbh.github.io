---
title: Merging a git branch
tags: git github 
---

If we want to merge the branch `remote_branch` to the branch `local_branch` (the terms `remote` and `local` are well-defined in that sense), we do the following.

* Create a branch

```
git branch local_branch
```

* Checkout to the (`local`) branch using

```
git checkout local_branch
```

* Merge the other branch (`remote`) to the current one (`local`)

```
git merge remote_branch
```

**Note:** you may get 'branch does not exist' error, in that case, `checkout` to the remote branch first and then get back to the local one.

* Merge conflicts will arise which can be resolved with launching a diffing tool with

```
git mergetool
```

- Delete the remote branch

```
git branch -d remote_branch
```

- Delete the remote branch on origin (remote)

```
git push -d origin remote_branch
```


### Replacing _all_ files without resolving conflicts

* **See below for alternative** ~~ To replace all the local files with the remote files, do 
```
git merge --strategy-option theirs
```
* To keep local files and discard the remote files while merging do
```
git merge --strategy-option ours
```
~~

**Caution:** Better alternative is to go through `git mergetool` and open it with `vimdiff` and then
- Make the remote branch the final version with `:%diffget RE`
- Make the local  branch the final version with `:%diffget LO`

### Using `vimdiff` as a mergetool:

* **Caution:** Quit unfinished merging work with `:cquit` (or `:cq`, to exit with an error code) so that next time `git mergetool` will launch `vimdiff` again. Otherwise, the file is all messed up with strings like `HEADER >>>>>>` and is saved as a real file and `mergetool` does not do anything.

If you quit `vimdiff` midway and would like to reset the merge again, 

1. first cancel the merge

```
git reset --merge
```

2. and perform the merge again with

```
git merge remote_branch
```

3. fix merge conflicts

```
git mergetool
```

or with 

```
git mergetool tool=vimdiff
```

if git is not configured.

- Resize vimdiff window after maximizing using `Ctrl+w =`

* There are 3 windows on top:
	- left: local: the file from the branch we are current staying, i.e. the local branch
	- right: remote: the file from the branch from which we are merging, the remote branch
	- middle: base: a common ancestor of both local and remote from which both of the files were originated and diverted

Bottom window: final version of the merged file in the local branch, after merging

* We navigate in the bottom file (using `[c` and `]c`), changing lines if needed. To add changes from the remote version (i.e. from branch `remote_branch`), do `:diffget RE`
Alternatively, `BA` or `LO` for base or local.
* To apply the same change to the _whole_ file:
- Make the final version of the file same as the remote copy with `:%diffget RE`:
- Make the final version of the file same as the local copy with `:%diffget LO`
* If the lines get misaligned, do `:diffupdate`

* After merging is done, save the final version (Bottom window) of the file and quit.
* Git `.orig` files using `git clean -fd` 
- Might need to add the file again using `git add filename` (check if this is needed with `git status`)
* Commit the current branch with `git commit -m 'merged remote_branch with local_branch'`
* Delete the branch that is merged with the current (local) branch using

```
git branch -d remote_branch
```

**Caution:** attempting to delete the remote branch without committing the merged local branch first will throw warning sign. That would be a reminder that the current needs to to committed.

## Scenarios

### Pull from the internet and discard your local changes:

```
git reset --hard
git clean -f
git pull
```

Here, `clean -f` to remove untracked files. `clean -fd` deletes untracked directories as well. Before `clean -f`, we can do `clean -d` to see which files are to be removed.

### Pull from the internet and set aside the local (uncommited) changes:

```
git stash
git pull
```

Then to pop back the local uncommitted changes on top of that using

```
git stash pop
```

To delete the stash, do `git stash drop` instead.

**Desired Method**: Pull from the internet and put the current __committed__ changes as next commit after the remote version
[(nice explanation for the reason to rebase)](https://megakemp.com/2019/03/20/the-case-for-pull-rebase/)

```
git pull --rebase
```

(or just `git pull -r`)

This might need merge-conflict resolution 

```
git mergetool --tool=vimdiff
```

and cleanup 

```
git clean -df
```

Then, to indicate that rebasing is done, we do

```
git rebase --continute
```

followed by `git push` to push the final local change. (Note that  `git commit` is not required and has been done automatically)

This creates a commit history of the order `last remote commit, merged local commit`.

This (`--rebase`) is better for history and creates 2 commit histories compared to just `git pull` (with default `--merge` behavior), which creates 3 commit histories in the order `last remove commit, last local commit, merged commit`.

To recover from a failed `rebase` and revert to the state before the attempted `pull` (i.e. local changes remain in local directory), do

```
git rebase --abort
```

**Note**: `git pull --rebase` should be used over just `git pull` where we do not want to advertise that a merging has been done, e.g. when working on the same branch. This is the most common scenario.


* See the difference between file in two different branches

```
git diff branch_1 branch_2 -- filename.txt
```

The output will have the following:
 * Common lines are in white
 * Lines in branch_1 (and not in branch_2) are in red (and with `-`)
 * Lines in branch_2 (and not in branch_1) are in green (and with `+`)
To use `vimdiff`, replace `git diff` with `git difftool`.

* To change a conflicted file (with conflict markers) into the state of its last commit, do `git restore filename`

* See the commit history _of the current branch_

```
git log
```

or with ` git log -p ` to see all the changes (patches) to files. Other useful options are `--pretty=oneline` or `stat`.

* Delete `.orig` files (record of merging) after merging is done using

```
git clean -fd
```

* Maintain  empty directories in your repository by creating `.gitkeep` file (conventional name)

```
touch empty_dir/.gitkeep
```

and tell to `.gitignore` to not ignore it using

```
# Inside .gitignore
empty_dir/*
!empty_dir/.gitkeep
```

* `git rebase` linearizes two diverging branch heads. If we have a diverging branch `exp` of the `main` branch, we can do

```
git checkout exp
git rebase main
```

to make the changes of `exp` as a next commit to the ones in `main`. At this point, the last commit of `main` becomes a previous commit for `exp`. So, we can just merge `exp` to `main` using

```
git checkout main
git merge exp
```

**Q**: How to change files with conflict markers to its state before attempted merge?

```
git merge --abort
```

Note, for uncommitted files, this might revert the files back to last committed state.

