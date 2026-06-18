## Task 1: Git Merge — Hands-On
1. Create a new branch feature-login from main, add a couple of commits to it
2. Switch back to main and merge feature-login into main
3. Observe the merge — did Git do a fast-forward merge or a merge commit?
4. Now create another branch feature-signup, add commits to it — but also add a commit to main before merging
5. Merge feature-signup into main — what happens this time?
6. Answer in your notes:
- What is a fast-forward merge?
- When does Git create a merge commit instead?
- What is a merge conflict? (try creating one intentionally by editing the same line in both branches)

```bash
git checkout -b feature-login
echo "Checking bug in login feature" >> login-feature-test-1.js
echo "fixed bug in login feature" >> login-feature-test-1.js
git add login-feature-test-1.js
git commit -m "login feature fixed"
git switch master
git merge feature-login

Git performed a Fast-Forward merge because the master branch had no new commits, so Git simply moved the master pointer to the latest commit of feature-login.


git checkout -b signup-feature
echo "fixed signup feature" >> signup-feature-test-1.js
git add signup-feature-test-1.js
git commit -m "signup-feature-test-1.js"
git switch master
echo "testing bug fixed in signup feature" >> signup-feature-test-v1.js
git add signup-feature-test-v1.js
git commit -m "signup-feature-test-v1.js"
git merge signup-feature
Merge made by the 'ort' strategy.
 signup2.js | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 signup2.js

Git creates a Merge Commit when both master and feature-signup had independent commits before the merge.
```


## Task 2: Git Rebase — Hands-On
1. Create a branch feature-dashboard from main, add 2-3 commits
2. While on main, add a new commit (so main moves ahead)
3. Switch to feature-dashboard and rebase it onto main
4. Observe your git log --oneline --graph --all — how does the history look compared to a merge?
```bash
Rebase rewrites the feature branch commits on top of the latest main, producing a clean linear history, while Merge preserves both branch histories and creates a merge commit.
```
6. Answer in your notes:
- What does rebase actually do to your commits?
- How is the history different from a merge?
- Why should you never rebase commits that have been pushed and shared with others?
- When would you use rebase vs merge?
```bash


git checkout -b feature-dashboard
git commit -m "Add dashboard UI"   # D
git commit -m "Add charts"         # E
git commit -m "Add sidebar"        # F
A --- B --- C (main)
             \
              D --- E --- F (feature-dashboard)


git checkout main
git commit -m "Add hotfix"    # G
A --- B --- C --- G (main)
             \
              D --- E --- F (feature-dashboard)

At this point:
main moved ahead with G
feature-dashboard still has D,E,F

git checkout feature-dashboard
git rebase main
A --- B --- C --- G --- D' --- E' --- F'
✅ Linear history
✅ No merge commit
✅ Cleaner git log

-----------------------------------
Easy rule
Merge
git checkout X
git merge Y

= Merge Y INTO X

Rebase
git checkout X
git rebase Y

= Replay commits of X ON TOP OF Y
-----------------------------------




# Create feature branch
git checkout -b feature-dashboard

# Work and commit
git add .
git commit -m "Add dashboard UI"
git commit -m "Add charts"

# Before PR, sync with latest master
git fetch origin
git rebase origin/master

# Push updated branch
git push 

Above is usually done``, after you finish working on your feature-dashboard branch and before pushing the final changes or creating a Pull Request to master, you rebase your branch onto the latest master so that your feature branch contains the newest changes and has a clean, linear history.


```
```bash
1. What does git rebase actually do to your commits?

Suppose:
main:
A --- B --- C --- G

feature:
             \
              D --- E --- F

You run:

git checkout feature
git rebase main

Git does 3 things:

Temporarily removes your commits:
D E F
Moves the feature branch to the latest main:
A --- B --- C --- G
Replays your commits one by one:
A --- B --- C --- G --- D' --- E' --- F'

Notice:

D != D'
E != E'
F != F'

The commit hashes change.
That's why we say:
Rebase rewrites history by creating new versions of your commits on top of another branch.

2. How is history different from a Merge?
Merge
git checkout feature
git merge main

History:

                 M
               /   \
A --- B --- C --- G
             \
              D --- E --- F
Branch structure is preserved.
Merge commit M is created.

Rebase
git checkout feature
git rebase main

History:

A --- B --- C --- G --- D' --- E' --- F'
Linear history.
No merge commit.
Old commits replaced by new ones.

3. Why should you NEVER rebase commits that are already shared?

Imagine you pushed:
feature:
A --- B --- C --- D --- E

Your teammate pulled:
A --- B --- C --- D --- E

Now you run:
git rebase main

Git creates:
A --- B --- C --- G --- D' --- E'

and:
git push --force

Now:
GitHub has D' E'
Your teammate still has D E

Git sees:
D != D'
E != E'

Same changes.
Different commits.
This leads to:

Conflicts
Duplicate commits
Difficult merges
Example

Teammate:
A-B-C-D-E

Remote:
A-B-C-G-D'-E'

Now Git gets confused because:
D and D'
look like different commits.
Rule

Only Rebase local commits
Don't rebase public/shared commits

Safe Rule
If ONLY YOU use the branch
USE:
git rebase main
✅ Safe
Never rebase commits that other people already have, because rebase changes commit IDs and causes everyone's history to diverge.

4. When to use Rebase vs Merge?
Use Rebase
When:
Working on your own feature branch
Updating with latest main
Cleaning commit history
Before opening a Pull Request

Example:
git checkout feature
git fetch origin
git rebase origin/main

Result:
A-B-C-G-D'-E'-F'
Clean history.

Use Merge
When:
Combining completed features into main
Working with shared branches
You want to preserve branch history

Example:
git checkout main
git merge feature

Result:

         M
       /   \
A-B-C-G    |
     \     |
      D-E-F
Use Rebase on your own private feature branches to keep history clean. Use Merge on shared branches to preserve history and avoid disrupting other collaborator
```



## Task 3: Squash Commit vs Merge Commit
1 Create a branch feature-profile, add 4-5 small commits (typo fix, formatting, etc.)
2 Merge it into main using --squash — what happens?
3 Check git log — how many commits were added to main?
4 Now create another branch feature-settings, add a few commits
5 Merge it into main without --squash (regular merge) — compare the history
Answer in your notes:
- What does squash merging do?
- When would you use squash merge vs regular merge?
- What is the trade-off of squashing?







```bash
Part 1: Create feature-profile branch
Step 1: Create and switch to the branch
git checkout -b feature-profile
Step 2: Create 5 small commits
Commit 1
touch profile.html
git add .
git commit -m "Add profile page"
Commit 2
touch typo.js
git add .
git commit -m "Typo fix"
Commit 3
touch formatting.css
git add .
git commit -m "Formatting"
Commit 4
touch bugfix.js
git add .
git commit -m "Bug fix"
Commit 5
touch image.png
git add .
git commit -m "Add profile image"
Check history
git log --oneline

You will see something like:

a1b2c3 Add profile image
d4e5f6 Bug fix
g7h8i9 Formatting
j1k2l3 Typo fix
m4n5o6 Add profile page

There are 5 commits.

Part 2: Squash merge into main

Switch to main:

git checkout main

Now squash merge:

git merge --squash feature-profile

Git says:

Squash commit -- not updating HEAD

This means:

Git collected all 5 commits and prepared them as ONE big change.

Now commit:

git commit -m "Add profile feature"
Check history
git log --graph --oneline --all

You will see:

* abc123 Add profile feature
| * a1b2c3 Add profile image
| * d4e5f6 Bug fix
| * g7h8i9 Formatting
| * j1k2l3 Typo fix
| * m4n5o6 Add profile page
Important

On main, only:

Add profile feature

appears.

So:

How many commits were added to main?

✅ Only 1 commit

Even though the feature branch had 5 commits.

Part 3: Create another branch
git checkout -b feature-settings

Create 3 commits

touch settings.html
git add .
git commit -m "Add settings page"
touch theme.css
git add .
git commit -m "Add theme"
touch settings.js
git add .
git commit -m "Add settings logic"
Merge WITHOUT squash

Go back:

git checkout main

Merge:

git merge feature-settings
Check history
git log --graph --oneline --all

You may see:

* aaaa111 Add settings logic
* bbbb222 Add theme
* cccc333 Add settings page
* dddd444 Add profile feature

OR

* eeee555 Merge branch 'feature-settings'
|\
| * aaaa111 Add settings logic
| * bbbb222 Add theme
| * cccc333 Add settings page
|/
* dddd444 Add profile feature
Comparison
Squash Merge

Before:

feature-profile

A
B
C
D
E

After:

main

F (contains A+B+C+D+E)

Only one commit.

Regular Merge

Before:

feature-settings

A
B
C

After:

main

Merge Commit
   / \
  A-B-C

All commits remain visible.

Answer these notes
What does squash merging do?

Squash merge combines multiple commits from a feature branch into a single commit before adding it to the target branch.

Example:

Feature:

A -> B -> C -> D

After squash:

main:

X

where X contains all changes from A+B+C+D.

When would you use squash merge?

Use squash merge when:
Feature branch has many small commits
Commits like:
typo fix
formatting
test
debug
You want a clean main branch history

Example:
Bad main:
fix typo
fix typo again
debug
remove console
formatting
actual feature

Better:
Add User Profile Feature
When would you use regular merge?

Use regular merge when:
You want the full development history.
Multiple developers worked on the branch.
Every commit is meaningful.
You may need to trace bugs later.

- What is the trade-off of squashing?
Pros
Cleaner git history
Easier to read
Main branch stays concise

Cons
Individual commit history is lost on main.
You cannot easily see:
when the typo was fixed
when formatting happened
when a bug fix was introduced

So the trade-off is:
Clean history vs Detailed history

Squash = clean but less detailed.
Regular merge = detailed but can become messy.
```

# Task 4: Git Stash — Hands-On
1 Start making changes to a file but do not commit
2 Now imagine you need to urgently switch to another branch — try switching. What happens?
3 Use git stash to save your work-in-progress
4 Switch to another branch, do some work, switch back
5 Apply your stashed changes using git stash pop
6 Try stashing multiple times and list all stashes
7 Try applying a specific stash from the list
Answer in your notes:
- What is the difference between git stash pop and git stash apply?
- When would you use stash in a real-world workflow?

```bash
# Task 4: Git Stash — Hands-On

## Objective

Learn how to temporarily save uncommitted changes using `git stash`, switch branches safely, and restore the changes later.

---

## Step 1: Start making changes but do not commit

Switch to your feature branch:

```bash
git switch feature-profile
```

Create or modify a file:

```bash
echo "Working on login validation" > login.txt
```

Check status:

```bash
git status
```

Output:

```text
modified: login.txt
```

Do **not** commit.

---

## Step 2: Try switching to another branch

```bash
git switch main
```

Possible output:

```text
error: Your local changes to the following files would be overwritten by checkout:

login.txt

Please commit your changes or stash them before you switch branches.
```

### Why did this happen?

Git is protecting your uncommitted work from being overwritten by files in the target branch.

---

## Step 3: Save work using git stash

```bash
git stash
```

If you also have untracked files:

```bash
git stash -u
```

Output:

```text
Saved working directory and index state WIP on feature-profile
```

---

## Step 4: Switch to another branch

```bash
git switch main
```

Now Git allows the switch because your working directory is clean.

---

## Step 5: Do some work on main

```bash
echo "Fix signup bug" > signup.txt

git add signup.txt
git commit -m "Fix signup bug"
```

---

## Step 6: Return to feature branch

```bash
git switch feature-profile
```

---

## Step 7: Restore stashed changes

```bash
git stash pop
```

Your previous work returns:

```text
login.txt

Working on login validation
```

---

## Step 8: Create multiple stashes

```bash
echo "First stash" > file1.txt
git stash

echo "Second stash" > file2.txt
git stash

echo "Third stash" > file3.txt
git stash
```

---

## Step 9: List all stashes

```bash
git stash list
```

Example:

```text
stash@{0}: WIP on feature-profile
stash@{1}: WIP on feature-profile
stash@{2}: WIP on feature-profile
```

---

## Step 10: Apply a specific stash

```bash
git stash apply stash@{1}
```

This restores the selected stash but keeps it in the stash list.

---

# Notes

## What is the difference between `git stash pop` and `git stash apply`?

### git stash pop

* Restores the stashed changes.
* Removes the stash entry after applying.

Example:

```bash
git stash pop
```

After this, the stash is deleted.

---

### git stash apply

* Restores the stashed changes.
* Keeps the stash entry in the stash list.

Example:

```bash
git stash apply stash@{0}
```

Useful if you want to reuse the stash later.

---

## When would you use stash in a real-world workflow?

You use `git stash` when:

* You are working on a feature and the work is incomplete.
* An urgent production bug needs to be fixed on another branch.
* You do not want to create a temporary or incomplete commit.
* You need a clean working directory to switch branches or pull changes.

### Example

You are developing a login feature on `feature-login`.

Before completing it, your manager asks you to fix a signup bug on `main`.

Workflow:

```bash
git stash
git switch main

# Fix bug
git commit -m "Fix signup issue"

git switch feature-login
git stash pop
This allows you to temporarily pause your work and continue later without losing any changes.
```





## Task 5: Cherry Picking
1 Create a branch feature-hotfix, make 3 commits with different changes
2 Switch to main
3 Cherry-pick only the second commit from feature-hotfix onto main
4 Verify with git log that only that one commit was applied
5 Answer in your notes:
- What does cherry-pick do?
- When would you use cherry-pick in a real project?
- What can go wrong with cherry-picking?
```bash
# Task 5: Cherry Picking

## What does cherry-pick do?

`git cherry-pick` copies a specific commit from one branch and applies it to another branch without merging the entire branch.

Example:

```text
feature-hotfix

A -> B -> C


main

X
```

Cherry-picking commit **B**:

```bash
git cherry-pick <hash-of-B>
```

Result:

```text
main

X -> B'
```

Only commit **B** is copied.

---

## When would you use cherry-pick in a real project?

### 1. Urgent Production Bug Fix

Suppose:

```text
feature-login

Commit 1 -> UI Changes
Commit 2 -> Critical Login Bug Fix
Commit 3 -> Refactoring
```

Production is down.

You only need:

```text
Critical Login Bug Fix
```

Instead of merging the whole branch:

```bash
git switch main
git cherry-pick <commit-hash>
```

Only the bug fix is copied to `main`.

---

### 2. Reuse a Specific Change

If you made a useful configuration or utility change on one branch and want it on another branch without merging everything, cherry-pick is a good option.

---

## What can go wrong with cherry-picking?

### 1. Merge Conflicts

If the same file is changed differently on both branches:

```text
main

login.js
Version A


feature-hotfix

login.js
Version B
```

Cherry-picking may result in:

```text
CONFLICT (content): Merge conflict in login.js
```

You must resolve the conflict manually.

---

### 2. Duplicate Commits

Cherry-picking creates a new commit with a different hash.

Example:

```text
feature-hotfix

a1b2c3 Fix login bug
```

After cherry-pick:

```text
main

d4e5f6 Fix login bug
```

Same change, different commit hash.

This can make commit history more difficult to understand.

---

### 3. Missing Dependencies

Sometimes a commit depends on earlier commits.

Example:

```text
Commit A -> Create login.js
Commit B -> Add validation in login.js
```

If you cherry-pick only Commit B:

```text
Fix login.js
```

Git may fail because:

```text
login.js does not exist on the target branch.
```

Commit B depends on Commit A.

---

## Summary

* Cherry-pick copies a specific commit to another branch.
* Useful for hotfixes and selective changes.
* Does not merge the entire branch.
* Can cause merge conflicts, duplicate commits, or dependency issues if used incorrectly.
```



