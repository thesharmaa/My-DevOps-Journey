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

Git created a Merge Commit because both master and feature-signup had independent commits before the merge.
```
