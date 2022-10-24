# Introduction

# Git-Hooks

Git can fire off custom scripts when certain important actions occur.

1. pre-commit
2. prepare-commit-msg
3. commit-msg
4. post-commit

We can bypass pre-commit and commit-msg hooks using the following command:

```shell
git commit -m "tidy" --no-verify
```

# Commands

1. Create and switch to a new branch

```shell
git switch -c path_config
# Switched to a new branch 'path_config'
```



#### Need to clean up .....


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
git branch -d <branch>
```

If the branch test_dev_branch is not fully merged you will get an error but you can force delete it using -D instead of -d

```
git branch -D <branch>
```

Delete test_dev_branch from remote

```
git push origin --delete <branch>
```

4. Pull from master into the development branch

```
git checkout test_dev_branch # gets you on test_dev_branch
git fetch origin             # gets you up to date with origin
git merge origin/master
```

5. Switch to another branch

```
git checkout <branch>
```

6. Create a new branch

```
git branch <branch>
```

7. Git squash

Last three commits

```
git rebase -i HEAD~3
```

change the file

```
pick 12345 Commit 1
squash 54321 Commit 2
squash 98765 Commit 3
```

save and quit

```
fix the commit message
```

push

```
git push origin DEV-244 -f
```

8. Empty directorie

https://git.wiki.kernel.org/index.php/GitFaq#Can_I_add_empty_directories.3F

9. Remove .gitignore files from github

```
git rm -rf --cached .
git commit -m "rm files"
git push
```


10. 

```shell
git rm -r --cached .
```
