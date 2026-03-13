# Homework #1: Git Workflow and History Management

> Practicing Git workflow and history management — from initializing a repo to recovering lost commits and pushing to GitHub.

\---

## Objectives

* Initialize a Git repository
* Create commits with unclear messages
* Clean up commit history using interactive rebase
* Simulate and recover a lost commit
* Create a branch from the recovered commit
* Define a custom Git alias
* Tag a cleaned version as `v1.0`
* Push the repository to GitHub

\---

## Steps

### Step 1 — Initialize the Repository

```bash
mkdir git-homework
cd git-homework
git init
```

\---

### Step 2 — Create the Project File and Make Unclear Commits

```bash
# First commit
echo "Version 1" > project.txt
git add project.txt
git commit -m "update"

# Second commit
echo "Added second line" >> project.txt
git add project.txt
git commit -m "stuff"

# Third commit
echo "Added third line" >> project.txt
git add project.txt
git commit -m "final"
```

\---

### Step 3 — Clean Up Commit History

Use interactive rebase to squash all commits into one meaningful commit:

```bash
git rebase -i --root
```

Combined all commits into a single commit with the message:

```
Initial project setup and file updates
```

\---

### Step 4 — Simulate a Lost Commit

```bash
echo "This is a lost change" >> project.txt
git add project.txt
git commit -m "Add lost work"
```

\---

### Step 5 — Remove the Commit

```bash
git reset --hard HEAD\\\~1
```

\---

### Step 6 — Recover the Lost Commit Using Git Reflog

```bash
git reflog
```

Recovered commit found in reflog:

```
46e66d7 commit: Add lost work
```

\---

### Step 7 — Create a New Branch from the Recovered Commit

```bash
git checkout -b recovered-work 46e66d7
```

\---

### Step 8 — Define a Custom Git Alias

```bash
git config --global alias.hist "log --oneline --graph --decorate --all"
```

Run the alias:

```bash
git hist
```

Example output:

```
\* 0801a36 (HEAD -> main, origin/main) Add README documentation

| \* 46e66d7 (origin/recovered-work, recovered-work) Add lost work

|/

\* 923f84c (tag: v1.0) Initial project setup and file updates```

\---

### Step 9 — Tag the Cleaned Version as `v1.0`

```bash
git checkout main
git tag v1.0
```

\---

### Step 10 — Push Everything to GitHub

```bash
git remote add origin https://github.com/dafinaak/git-homework.git
git push -u origin main
git push -u origin recovered-work
git push origin v1.0
```

\---

## Command Summary

|Command|Purpose|
|-|-|
|`git init`|Initialize a new repository|
|`git add` / `git commit`|Stage and save changes|
|`git rebase -i --root`|Squash commits interactively|
|`git reset --hard HEAD\\\~1`|Remove the last commit|
|`git reflog`|View full history including lost commits|
|`git checkout -b recovered-work 46e66d7`|Create a branch from a specific commit|
|`git config --global alias.hist "log --oneline --graph --decorate --all"`|Define a custom Git alias|
|`git tag v1.0`|Tag a specific commit|
|`git push`|Upload branches and tags to GitHub|



