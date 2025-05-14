1. Revert the main branch to a previous commit

2. Create and switch to a new branch

```shell
git switch -c path_config
# Switched to a new branch 'path_config'
```

3. List all local branches

```shell
git branch --all
```

4. List all the remote brances

```shell
git branch -r
```

5. Reset all changes after last commit

Undo chnages to tracked file:

```shell
git reset HEAD --hard
```

6. Remove GIT History (Caution it delete all the commit history)

```shell
git checkout --orphan last
git add -A
git commit -am "fresh init"
git branch -D main
git branch -m main
git push -f origin main
```

7. Bare repository

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
```

8. Log

```shell
git log --oneline
```

9. Git bisect

```shell
git bisect start
git bisect bad
git bisect good
```

10. Reduce Git repository size

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
bfg --strip-blobs-bigger-than 1M binarytree.git
cd binarytree.git
```

11. Revert


```shell
A---B---C---D---E (develop)
         \ 
          F---G (feature branch)
               \
                H (merge commit: 9343dSwd)
```

H has two parents:

Parent 1: commit E (mainline — usually develop)

Parent 2: commit G (feature branch)

```shell
git revert -m 1 H
```

Git will:

- Keep the content as it was in E
- Undo the changes from the feature branch (G)
- Create a new commit that undoes the merge.
