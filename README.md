# Git-Helper

1. How do I reset master to origin/master?

If -B is given, <new_branch> is created if it doesn’t exist; otherwise, it is reset.
```
git checkout -B master origin/master
```


2. Rollback a Git merge

With git reflog check which commit is one prior the merge 

```
git reset --hard commit_sha
```
