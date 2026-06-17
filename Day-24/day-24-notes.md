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





















