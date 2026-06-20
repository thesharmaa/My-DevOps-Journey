## Task 1: Git Reset — Hands-On
1. Make 3 commits in your practice repo (commit A, B, C)
2. Use git reset --soft to go back one commit — what happens to the changes?
3. Re-commit, then use git reset --mixed to go back one commit — what happens now?
4. Re-commit, then use git reset --hard to go back one commit — what happens this time?
Answer in your notes:
- What is the difference between --soft, --mixed, and --hard?
- Which one is destructive and why?
- When would you use each one?
- Should you ever use git reset on commits that are already pushed?
```bash
1. - Removes the latest commit 
- Keeps all changes in staging area
- Working directory remains unchanged
- Changes are ready to be recommitted immediately


2. - Removes the latest commit 
- Removes changes from staging area
- Keeps changes in working directory as modified files
- Need to run `git add` again before commit


3. - Removes the latest commit 
- Removes changes from staging area
- Deletes changes from working directory completely
- All work done in commit C is lost


4. What is the difference between --soft, --mixed, and --hard?
- `--soft` → only commit is removed, changes stay staged
- `--mixed` → commit removed, changes unstaged
- `--hard` → commit removed + all changes deleted

5.Which one is destructive and why?
- `--hard` is destructive
- Because it permanently deletes changes from both staging area and working directory

6. When would you use each one?
- `--soft` → combine commits or redo commit message
- `--mixed` → undo commit but review/edit changes
- `--hard` → discard all changes and reset to last stable state


7. Should you use git reset on pushed commits?
- Generally NO
- It rewrites commit history and can break shared repository history
- Use `git revert` instead for commits already pushed
```

# Task 2: Git Revert — Hands-On
1 Make 3 commits (commit X, Y, Z)
2 Revert commit Y (the middle one) — what happens?
3 Check git log — is commit Y still in the history?
Answer in your notes:
1. How is git revert different from git reset?
2 Why is revert considered safer than reset for shared branches?
3 When would you use revert vs reset?


```bash
# Task 2: Git Revert — Hands-On Notes

## 2. What happens when you revert commit Y (middle commit)?

- Git creates a **new commit** that undoes the changes of commit Y
- The effect of Y is removed from the project
- Other commits (X and Z) remain unchanged
- Sometimes conflicts can happen if later commits depend on Y

---

## 3. Is commit Y still in the history?

- YES
- Commit Y is still present in `git log`
- Only its effects are undone, not the commit itself

---

## 4. How is `git revert` different from `git reset`?

- `git revert`:
  - Does NOT delete commit history
  - Creates a new commit that undoes changes
  - Safe for shared repositories

- `git reset`:
  - Moves branch pointer backward
  - Can remove commits from history
  - Rewrites commit history

---

## 5. Why is revert safer than reset for shared branches?

- It does not delete existing commits
- It preserves history for all developers
- No force push is required
- Avoids breaking other team members' repositories

---

## 6. When would you use revert vs reset?

### Use `git revert` when:
- Commits are already pushed to remote
- Working on shared/team branches (main, develop)
- You want safe undo without changing history

### Use `git reset` when:
- Working locally before pushing
- Cleaning up or reorganizing commits
- Combining or removing commits in private branch
```
# Task 3: Reset vs Revert — Summary
```bash
# Git Reset vs Git Revert Comparison

| Feature | git reset | git revert |
|--------|-----------|-------------|
| What it does | Moves branch pointer backward and can change staging/working directory | Creates a new commit that undoes changes of a previous commit |
| Removes commit from history? | Yes (history is rewritten depending on mode) | No (commit stays in history) |
| Safe for shared/pushed branches? | ❌ No (can break history, requires force push) | ✅ Yes (does not rewrite history) |
| When to use | Local commits, before push, rewriting or cleaning history | After push, in shared branches, safely undo changes |
```

# Brnching strategy
```bash
# Branching Strategies

---

## 1. GitFlow

GitFlow uses multiple long-lived branches:
- main → Production-ready code
- development →
- features
- release
- hotfix

In GitFlow you typically start with main branch. From there, you create a development branch. All the feature branches branch off from develop, & once a feature is ready, it gets merged back to development branch.

Now, when we are ready for release we create a release branch off of development branch.

After it's stable, we merge it into main, and also back to development to keep things in sync.

---

It is used because it provides a clear, organized process for releases. Each release branch is a stable snapshot which helps with scheduled rollouts, audits & compliance & something critical in industries like banking or healthcare.

---

## 2. GitHub Flow

There is only one permanent branch → main or master.
- Developer creates a feature branch from main.
- Commit changes
- Open a pull request
- Review & merge into main.
- Deploy immediately.

It is used in Startups, SAAS products, web applications or teams deploying multiple times a day. It is very simple.

---

## 3. Trunk-Based Development (TBD)

Everyone works on main → Also called as Trunk.

Feature branches are:
- Very short lived (hours or 1-2 days)
- Merged frequently.

It is used in companies practicing CI/CD
- High-performing DevOps teams
- Continuous deployment environments.

★ It provides fastest integration.
★ Fewer merge conflicts.
★ Encourages continuous integration.
★ Faster releases.

---

★ Best strategy for startup shipping fast?
→ GitHub Flow.
Because: Simple workflow, Fast Deployment, Ideal for frequent releases & small teams.

★ Which strategy for large team with scheduled releases?
→ GitFlow.
Reason: → Dedicated development, release & hotfix branches
→ Better control over releases
→ Easier version management for enterprise software
```



