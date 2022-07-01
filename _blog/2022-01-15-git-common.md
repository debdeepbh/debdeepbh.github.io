---
title: Common git scenarios
tags: git github 
---

## Removing a large file from the commit history

If you want to remove a large file from the repository which was accidentally committed and pushed to GitHub (possibly due to a sloppy `.gitignore`), do

```bash
git filter-branch --force --index-filter \
 'git rm --cached --ignore-unmatch path/to/file.jpg' \
 --prune-empty --tag-name-filter cat -- --all
```

Then, to delete the same in the remote repo,

```
git push origin --force --all
```


* If it is a directory the needs removal, use `rm -r ...` instead of `rm`.



## Removing sensitive information from github repo

[Main article](https://docs.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository)

## To change the email address of all previous commits

```
git filter-branch -f --commit-filter '
     if [ "$GIT_AUTHOR_EMAIL" = "OLD_EMAIL" ];
     then
             GIT_AUTHOR_EMAIL="NEW_EMAIL";
             git commit-tree "$@";
     else
             git commit-tree "$@";
     fi' HEAD
```

Then, force push the repo with

```
git push --force
```


