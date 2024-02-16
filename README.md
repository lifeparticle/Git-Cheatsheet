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

2. List all local branches

```shell
git branch --all
```


3. List all the remote brances

```shell
git branch -r
```

4. Reset all changes after last commit

Undo chnages to tracked file:

```shell
git reset HEAD --hard
```

Remove untracked files:

```shell
git clean -f
```

Remove untracked files and directories:

```shell
git clean -fd
```

Remove GIT History (Caution it delete all the commit history)

```shell
git checkout --orphan last
git add -A
git commit -am "fresh init"
git branch -D main
git branch -m main
git push -f origin main
```

5. Bare repository

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
```

[source](https://git-scm.com/docs/gitglossary.html#def_bare_repository)

6. Reduce Git repository size

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
bfg --strip-blobs-bigger-than 1M binarytree.git
cd binarytree.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
```

------------

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

# Resources

- https://www.youtube.com/watch?v=aolI_Rz0ZqY&ab_channel=GitButler
