```bash
<<commands
Here are the list of git commands
commands

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
git clone REPO_LINK "Downloads a remote repo to your local machine"
git restore --staged FILE_NAME "Moving file from staged to unstaged"
git diff "Shows unstaged changes"
git diff --staged "Shows unstaged changes"
git merge BRNACH_NAME "Merges another branch into current branch"
git stash "Temporarily saves uncommited changes"
git stash pop "Restore stashed changes"
git branch -a "Shows both local and remote branches."
git log --oneline --decorate --all "See all commits from all branches along with branch names and HEAD pointers in a compact view."
git push origin --all "Pushes all the local branches to github"
git push origin --delete BRANCH_NAME "To delete a branch"
git log --graph --oneline --decorate --all → "Used to visualize commit history, branches, and merges."
git reflog → "Used to track local HEAD movements and recover commits after operations like rebase, reset, or checkout."
git stash "Saves Tracked files only"
git stash -u "Saves Tracked + Untracked files only"
git stash pop "restores the changes and removes the stash entry if the operation succeeds"
git stash apply "estores stashed changes without deleting the stash"
git ls-files "To view tracked files"









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
