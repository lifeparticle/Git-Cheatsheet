* [0. Working Directory vs. Git's Knowledge](#0-working-directory-vs-gits-knowledge)
  + [1. Working Directory](#1-working-directory)
  + [2. What Git Tracks](#2-what-git-tracks)
    - [a. Staging Area - A temporary space for changes you plan to commit. Add files with:](#a-staging-area---a-temporary-space-for-changes-you-plan-to-commit-add-files-with)
    - [b. Local Repository - A permanent record of committed changes. Save changes with:](#b-local-repository---a-permanent-record-of-committed-changes-save-changes-with)
  + [The 3-State Model](#the-3-state-model)
  + [Workflow](#workflow)
  + [Example](#example)
* [2. Global Configuration](#1-global-configuration)
* [3. Initialize a Repository](#2-initialize-a-repository)
* [4. Check Repository Status](#3-check-repository-status)
* [5. Stage Changes](#4-stage-changes)
* [6. Commit Changes](#5-commit-changes)
* [7. View Commit History](#6-view-commit-history)
* [8. Display Differences Between File Versions](#7-display-differences-between-file-versions)
* [9. Ignore Files with .gitignore](#8-ignore-files-with-gitignore)
         + [Example .gitignore:](#example-gitignore)
* [10. Keeping Empty Folders in Git](#9-keeping-empty-folders-in-git)
         + [🔧 Problem:](#🔧-problem)
         + [Solution: Use a placeholder file, like .git-keep](#solution-use-a-placeholder-file-like-git-keep)
         + [Example:](#example)
* [11. Modify the Last Commit Without Changing the Message](#10-modify-the-last-commit-without-changing-the-message)
* [12. Revert the main branch to a previous commit](#11-revert-the-main-branch-to-a-previous-commit)
* [13. Create and switch to a new branch](#12-create-and-switch-to-a-new-branch)
* [14. List all local branches](#13-list-all-local-branches)
* [15. List all the remote brances](#14-list-all-the-remote-brances)
* [16. Reset all changes after last commit](#15-reset-all-changes-after-last-commit)
* [17. Remove GIT History (Caution it delete all the commit history)](#16-remove-git-history-caution-it-delete-all-the-commit-history)
* [18. Bare repository](#17-bare-repository)
* [19. Git bisect](#18-git-bisect)
* [20. Reduce Git repository size](#19-reduce-git-repository-size)
* [21. Revert](#20-revert)
* [22. Recover deleted files](#recover-deleted-files)

# Essential Git Workflow: A Technical Guide

## 0. Working Directory vs. Git's Knowledge

### 1. Working Directory
Your project's folder on your computer, where you:
- Create and edit files
- Delete or move folders
💡 It’s your live workspace, but Git doesn’t automatically track changes here.

### 2. What Git Tracks
Git manages changes in two key areas:
#### a. **Staging Area** - A temporary space for changes you plan to commit. Add files with:

```bash
git add <filename>
```

#### b. **Local Repository** - A permanent record of committed changes. Save changes with:

```bash
git commit -m "message"
```

### The 3-State Model
| State              | Description                            | Commands            |
|--------------------|----------------------------------------|---------------------------|
| 🗂️ Working Directory | Your project’s current files on disk   | `ls`, `cat`      |
| 📝 Staging Area      | Changes queued for the next commit     | `git add`, `git status`       |
| 🏛️ Repository        | Versioned history of confirmed changes | `git commit`, `git log`       |

### Workflow

```text
Working Directory → Staging Area → Repository
   (edit files)     (git add)     (git commit)
```

### Example
1. Edit `README.md` → Git is unaware of changes.
2. Run `git add README.md` → Changes are staged.
3. Run `git commit -m "Update README"` → Changes are saved in the repository.

## 1. Global Configuration

Before using Git, configure your identity. These settings are stored globally and used for all repositories on your machine.

```bash
git config --global user.email "your_email@example.com"
git config --global user.name "your_name"
```

This sets your Git author information globally, ensuring that all commits reflect your name and email.

## 2. Initialize a Repository

To start tracking a project with Git, navigate to your project directory and initialize a new repository:

```bash
git init
```

This creates a `.git` directory in your project, establishing it as a Git repository. By default, Git also creates a primary branch named `main`.

## 3. Check Repository Status

Use the `git status` command to inspect the current state of the working directory and staging area:

```bash
git status
```

Example output:

```
On branch main
nothing to commit, working tree clean
```

This indicates that you are on the `main` branch and that there are no changes staged or unstaged.

## 4. Stage Changes

To add files to the staging area (preparing them for a commit):

```bash
git add <filename>   # Adds a specific file
git add .            # Adds all changes in the current directory
```

Files must be staged before they can be committed.

## 5. Commit Changes

Commit staged changes to the local repository:

```bash
git commit -m "Your commit message here"
```

You can also commit changes to already tracked files (i.e., previously committed files that have been modified) in one step:

```bash
git commit -am "Update tracked files with changes"
```

> [!IMPORTANT]
> `git commit -am` **only** works for files that Git is already tracking. New files must be staged with `git add` first.

Example:

```bash
echo "1. TODO_1" >> README.md
git add README.md
git commit -m "Add initial TODO entry"
```

Every time you make a commit, it's like taking a snapshot of your project's files exactly as they are at that moment in time. You're telling Git:

“This is a version I want to remember.”

Just like a time machine, Git lets you travel back to any previous commit. You can see what your project looked like, what changed, and why. This makes collaboration safe, debugging easier, and progress traceable.

## 6. View Commit History

To review the commit history of the current branch in a concise format:

```bash
git log --oneline
```

This displays a summarized list of commits, showing the short commit hash and message for each entry.

## 7. Display Differences Between File Versions

To inspect changes made to files since the last commit, use the `git diff` command. This allows you to see line-by-line differences between your working directory and the staging area (or the last commit).

```shell
git diff
```

## 8. Ignore Files with `.gitignore`

The `.gitignore` file tells Git which files or directories to ignore (not track) in your project. This is useful for excluding:

- **Build artifacts** (e.g., `dist/`, `build/`, `coverage/`)
- **Temporary or cache files** (e.g., `*.tmp`, `*.log`, `*.swp`)
- **Operating system files** (e.g., `.DS_Store`, `Thumbs.db`)

### Example `.gitignore`:

```shell
# Ignore all log files
*.log

# Ignore node_modules directory
node_modules/

# Ignore system files
.DS_Store

# Ignore compiled Python files
__pycache__/
*.pyc
```

Place the `.gitignore` file in the root of your repository. Git will respect the patterns and avoid tracking matching files.

## 9. Keeping Empty Folders in Git

By default, **Git does not track empty directories**. If a folder has no tracked files, it will be ignored entirely—even if it exists in your project structure.

### 🔧 Problem:
You want to keep a folder (e.g., `logs/`, `uploads/`, `data/`) in the repository even though it's currently empty or only used at runtime.

### Solution: Use a placeholder file, like `.git-keep`

### Example:

```bash
mkdir uploads/
touch uploads/.git-keep
git add uploads/.git-keep
git commit -m "Keep empty uploads directory"
```

This will ensure the `uploads/` directory is committed and remains in the repository.

## 10. Modify the Last Commit Without Changing the Message

If you need to update the last commit then simply make your edits, stage them with `git add`, and run one of the follwoing commands:

| Command                     | Effect                                       |
|----------------------------|----------------------------------------------|
| `git commit --amend`       | Amend last commit and open message editor    |
| `git commit --amend -m "..."` | Amend last commit with new message        |
| `git commit --amend --no-edit` | Amend last commit without changing message |

> [!IMPORTANT]
> `Always double-check with `git log` after amending to confirm the result.

## 11. Revert the main branch to a previous commit

todo

## 12. Create and switch to a new branch

```shell
git switch -c path_config
# Switched to a new branch 'path_config'
```

## 13. List all local branches

```shell
git branch --all
```

## 14. List all the remote brances

```shell
git branch -r
```

## 15. Reset all changes after last commit

Undo chnages to tracked file:

```shell
git reset HEAD --hard
```

## 16. Remove GIT History (Caution it delete all the commit history)

```shell
git checkout --orphan last
git add -A
git commit -am "fresh init"
git branch -D main
git branch -m main
git push -f origin main
```

## 17. Bare repository

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
```


## 18. Git bisect

```shell
git bisect start
git bisect bad
git bisect good
```

## 19. Reduce Git repository size

```shell
git clone --mirror git@github.com:lifeparticle/binarytree.git
bfg --strip-blobs-bigger-than 1M binarytree.git
cd binarytree.git
```

## 20. Revert


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

## 22. Recover deleted files

todo


## Resource
1. [Essential-git-commands-every-programmer-should-know](https://medium.com/data-science/essential-git-commands-every-programmer-should-know-fe96feb570ce)
