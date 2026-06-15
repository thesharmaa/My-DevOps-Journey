# Challenge Tasks
## Task 1: Understanding Branches

```bash
* **What is a branch in Git?**
  A branch is separate workspace where you can work on changes separately.

* **Why do we use branches instead of committing everything to main?**
  Branches let us develop and test features safely without affecting the main code.

* **What is HEAD in Git?**
  HEAD is a pointer to the current branch and latest commit you are working on.

* **What happens to your files when you switch branches?**
  Git updates your working files to match the selected branch's latest commit.

```

## Task 2: Branching Commands — Hands-On
## In your devops-git-practice repo, perform the following:

## List all branches in your repo
## Create a new branch called feature-1
## Switch to feature-1
## Create a new branch and switch to it in a single command — call it feature-2
## Try using git switch to move between branches — how is it different from git checkout?
## Make a commit on feature-1 that does not exist on main
## Switch back to main — verify that the commit from feature-1 is not there
## Delete a branch you no longer need
## Add all branching commands to your git-commands.md

```bash
ubuntu@ip-172-31-47-106:~$ git branch
* master

ubuntu@ip-172-31-47-106:~$ git checkout -b feature-1
Switched to a new branch 'feature-1'

ubuntu@ip-172-31-47-106:~$ git branch
* feature-1
  master

ubuntu@ip-172-31-47-106:~$ git checkout -b feature-2
Switched to a new branch 'feature-2'

ubuntu@ip-172-31-47-106:~$ git branch
  feature-1
* feature-2
  master

ubuntu@ip-172-31-47-106:~$ git switch feature-1
Switched to branch 'feature-1'

ubuntu@ip-172-31-47-106:~$ git branch
* feature-1
  feature-2
  master

ubuntu@ip-172-31-47-106:~$ touch feature-1.py

ubuntu@ip-172-31-47-106:~$ git add feature-1.py

ubuntu@ip-172-31-47-106:~$ git commit -m "feature ready in feature-1 branch"
[feature-1 fc9234c] feature ready in feature-1 branch
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 feature-1.py

ubuntu@ip-172-31-47-106:~$ git log --oneline
fc9234c (HEAD -> feature-1) feature ready in feature-1 branch
ef937f0 (origin/master, master, feature-2) files

```


## What is the difference between origin and upstream?

```bash
origin is usually your own remote repository, while upstream is the original repository you forked from.
```

## What is the difference between git fetch and git pull?
```bash
git fetch only downloads changes, while git pull downloads and merges them into the current branch.
```

## What is the difference between clone and fork?
```bash
Clone = Copying a repository from a remote server to your local machine.
Fork = Creating your own copy of someone else's repository on GitHub.
```
## When would you clone vs fork?
```bash
Clone when you want to work on a repository you already have access to.
Fork when you want to contribute to someone else's repository without direct write access.
```
## After forking, how do you keep your fork in sync with the original repo?
```bash
First, fetch the latest changes from the original repository (upstream), merge them into my local branch, and then push the updated branch to my fork (origin).

git remote add origin <your-fork-link>
git remote add upstream <original-repo-link>

git fetch upstream
git merge upstream/master
```






















