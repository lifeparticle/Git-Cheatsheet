# Git-Helper

1. How do I reset master to origin/master?

If -B is given, <new_branch> is created if it doesn’t exist; otherwise, it is reset

```
git checkout -B master origin/master
```


2. Rollback a Git merge

With git reflog check which commit is one prior the merge 

```
git reflog
git reset --hard commit_sha
```


3. Delete a local branch

Switch to another branch and delete test_dev_branch

```
git checkout master
git branch -d test_dev_branch
```

If the branch test_dev_branch is not fully merged you will get an error but you can force delete it using -D instead of -d

```
git branch -D test_dev_branch
```

Delete test_dev_branch from remote

```
git push origin --delete test_dev_branch
```

4. Pull from master into the development branch

```
git checkout test_dev_branch # gets you on test_dev_branch
git fetch origin             # gets you up to date with origin
git merge origin/master
```

5. Switch to another branch

```
git checkout [branch]
```
