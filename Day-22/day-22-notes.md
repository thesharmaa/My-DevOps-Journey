# Challenge Tasks
## Task 1: Install and Configure Git
## Verify Git is installed on your machine
## Set up your Git identity — name and email
## Verify your configuration

```bash
sudo apt-get install update
sudo apt-get install git

ubuntu@ip-172-31-38-86:~$ git --version
git version 2.53.0

ubuntu@ip-172-31-38-86:~$ git config --global user.name thesharmaa
ubuntu@ip-172-31-38-86:~$ git config --global user.email sharmaamanjsr@gmail.com
ubuntu@ip-172-31-38-86:~$ cat .gitconfig
[user]
        name = thesharmaa
        email = sharmaamanjsr@gmail.com

```


## Task 2: Create Your Git Project
## Create a new folder called devops-git-practice
## Initialize it as a Git repository
## Check the status — read and understand what Git is telling you
## Explore the hidden .git/ directory — look at what's inside

```bash
ubuntu@ip-172-31-38-86:~/devops-git-practice$ git init

ubuntu@ip-172-31-38-86:~/devops-git-practice$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

ubuntu@ip-172-31-38-86:~/devops-git-practice$ cd .git
ubuntu@ip-172-31-38-86:~/devops-git-practice/.git$ ls
HEAD  config  description  hooks  info  objects  refs

.git/
├── HEAD        -> Current branch pointer
├── config      -> Repo settings
├── hooks/      -> Automation scripts
├── info/       -> Extra repo info
├── objects/    -> Git database (commits/files)
└── refs/       -> Branches and tags

```

## Task 3: Create Your Git Commands Reference
## Create a file called git-commands.md inside the repo
## Add the Git commands you've used so far, organized by category:
## Setup & Config
## Basic Workflow
## Viewing Changes
## For each command, write:
## What it does (1 line)
## An example of how to use it

```bash
git --version "Displays the installed GIT version"
git init "Creates a new GIT rep in the current directory"
git config --global user.name YOUR_GIT_USERNAME "Sets your GIT username globally"
git config --global user.email YOUR_GIT_EMAIL "Sets your GIT email globally"
git status "Shows the current state of the repo"
git remote -v "Lists configured remote repo"
git remote add origin YOUR_GIT_REPO_HTTP_LINK "Adds a remote repo named origin"
git remote set-url origin https://PAT_CODE@github.com/REPO_LINK "Updates the remote rep for authentication"
git add FILE_NAME or git add . "Stages a specific file for commit or all new modified files"
git commit -m "COMMENT" "Creates a commit with a message"
git push origin master "Pushes local commits to the remote master branch"
git pull origin master --rebase or git pull origin master --no-rebase "Pulls remote changes and rebases local commits on top or merges them into the current branch"
git pull --rebase "Pulls from the tracked remote branch and rebases local commits"
git rebase --continue "Continues a rebase after resolving conflicts"
git log --oneline "Shows a commit history in a compact one-line format"
git checkout -b NEW_BRANCH_NAME or git checkout BRANCH_NAME "Creates and switches to a new branch or an existing branch"
git branch "List all the branches"


Fast-Forward - A fast forwards happens when local branch has no new commit and git can simply move the branch pointer forward.

Local:  A --- B
Remote: A --- B --- C
Result:
A --- B --- C "One straight road"
✅ No merge commit



Non-Fast Forward "Two roads diverged" - A non fast forwards situation occurs when both local and remote have different commits.

Git needs a merge or rebase before it can continue
Merge (--no-rebase)
Local:  A --- B --- D
Remote: A --- B --- C
Result:
A --- B --- C
      \
       D ---- M
✅ Creates merge commit M

Rebase (--rebase)
Local:  A --- B --- D
Remote: A --- B --- C
Result:

A --- B --- C --- D'


```

## Task 4: Stage and Commit
## Stage your file
## Check what's staged
## Commit with a meaningful message
## View your commit history

```bash
ubuntu@ip-172-31-38-86:~/devops-git-practice$ ls -a
.  ..  .git  git-commands.md
ubuntu@ip-172-31-38-86:~/devops-git-practice$ git add .
ubuntu@ip-172-31-38-86:~/devops-git-practice$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-commands.md

ubuntu@ip-172-31-38-86:~/devops-git-practice$ git commit -m "Adding git commands documentation"

[master (root-commit) 057bd83] Adding git commands documentation
 1 file changed, 52 insertions(+)
 create mode 100644 git-commands.md

ubuntu@ip-172-31-38-86:~/devops-git-practice$ git log --oneline
057bd83 (HEAD -> master) Adding git commands documentation

```

## Task 5: Make More Changes and Build History
## Edit git-commands.md — add more commands as you discover them
## Check what changed since your last commit
## Stage and commit again with a different, descriptive message
## Repeat this process at least 3 times so you have multiple commits in your history
## View the full history in a compact format

```bash
ubuntu@ip-172-31-38-86:~/devops-git-practice$ git log --oneline
432628b (HEAD -> master) Adding more commands
7ce6101 Updating git-commands.md with git restore command
3a1b05a Updating git-commands.md with git commands
057bd83 Adding git commands documentation


```


## Task 6: Understand the Git Workflow
## Answer these questions in your own words (add them to a day-22-notes.md file):

## What is the difference between git add and git commit?
## What does the staging area do? Why doesn't Git just commit directly?
## What information does git log show you?
## What is the .git/ folder and what happens if you delete it?
## What is the difference between a working directory, staging area, and repository?

```bash
1. What is the difference between git add and git commit?

Answer:
git add moves changes to the staging area, while git commit saves those staged changes in the local repository.

Example:

git add app.py
git commit -m "Added login feature"

Why?
Because you may modify many files but only want to commit selected changes.

2. What does the staging area do? Why doesn't Git just commit directly?

Answer:
The staging area lets you review and choose which changes will be included in the next commit.

Example:

You changed:

app.py
README.md
config.txt

But only want to commit app.py:

git add app.py
git commit -m "Added login logic"

Why?
Without a staging area, Git would commit all modified files together, reducing control over commits.

3. What information does git log show you?

Answer:
git log shows the history of commits including commit ID, author, date, and commit message.

Example:

git log --oneline

Output:

a1b2c3d Added login feature
f4g5h6i Initial commit

Why?
To track what changes were made, who made them, and when.

4. What is the .git/ folder and what happens if you delete it?

Answer:
.git/ is Git's database that stores commits, branches, configuration, and history.

Example:

ls .git

Output:

HEAD  config  objects  refs

Why?
Git needs this folder to track versions. If you delete .git/, the project files remain, but Git history, branches, and tracking are lost.

5. What is the difference between a Working Directory, Staging Area, and Repository?

Answer:

Working Directory → Staging Area → Repository
       git add          git commit

Example:

echo "Hello" >> app.py

File is in the Working Directory.

git add app.py

File moves to the Staging Area.

git commit -m "Updated app"

Changes are saved in the Repository.

Why?

Working Directory → Where you make changes.
Staging Area → Where you prepare selected changes.
Repository → Where Git permanently stores commit history.
```




