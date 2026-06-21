# Task 1: Install and Authenticate
- Install the GitHub CLI on your machine
- Authenticate with your GitHub account
- Verify you're logged in and check which account is active
- Answer in your notes: What authentication methods does gh support?
```bash
sudo apt-get update
sudo apt install gh -y
gh --version
gh auth login
gh auth status

- Browser login (OAuth) → default, most common
- Personal Access Token (PAT) → for scripts/automation
- SSH keys → for Git operations via SSH
```

# Task 2: Working with Repositories
- Create a new GitHub repo directly from the terminal — make it public with a README
- Clone a repo using gh instead of git clone
- View details of one of your repos from the terminal
- List all your repositories
- Open a repo in your browser directly from the terminal
- Delete the test repo you created (be careful!)
```bash
gh repo new
gh repo new my-test-repo --public --clone --add-readme   //Improvised version to create new repo
gh repo view OWNER_NAME/REPO_NAME   // View details of a repository
gh repo view     //View details of current repository
gh repo clone OWNER_NAME/REPO_NAME
gh repo list
gh repo delete OWNER_NAME/REPO_NAME    //gh repo delete thesharmaa/my-test-repo
```

# Task 3: Issues
- Create an issue on one of your repos from the terminal — give it a title, body, and a label
- List all open issues on that repo
- View a specific issue by its number
- Close an issue from the terminal
- Answer in your notes: How could you use gh issue in a script or automation?
```bash
First get into repository to create an issue
gh repo clone thesharmaa/my-test-repo

gh issue create --
gh issue create --title "Bug" --body "Need to fix Signup Page"      //Improvised version to create an issue

gh issue list //Lists all issue across all repos
gh issue list --repo thesharmaa/my-test-repo  // Issue for specific repo
gh issue list --state all    //List all issues including closed ones
gh issue view 1 // Opens issue #1
gh issue close 1   // Close issue #1


```

# Task 4: Pull Requests
- Create a branch, make a change, push it, and create a pull request entirely from the terminal
- List all open PRs on a repo
- View the details of your PR — check its status, reviewers, and checks
- Merge your PR from the terminal
- Answer in your notes:
1. What merge methods does gh pr merge support?
  gh pr merge supports --merge, --rebase and --squash
3. How would you review someone else's PR using gh?
   gh pr review PR_NO
```bash

git checkout -b feature/login

touch login.js
git add login.js
git commit -m "fixed login issue"

touch singup.js
git add singup.js
git commit -m "fixed singup issue"

gh pr create --base main --head feature/login --title "New bug fixed" --body "fixed Login and Signup page bug"
gh pr create --fill // auto-fills the PR title and body from your commits

gh pr list --state all

gh pr view 4 //View PR #4

gh pr view 4 --json title,author,state,reviewRequests,comments



gh pr list //list all the PRs
gh pr diff 4 //See code changes
gh pr review 4
gh pr merge 4  //Review PR by its unique number
```

# Task 5: GitHub Actions & Workflows (Preview)
- List the workflow runs on any public repo that uses GitHub Actions
- View the status of a specific workflow run
- Answer in your notes: How could gh run and gh workflow be useful in a CI/CD pipeline?
```bash
Will complete after completing Github actions
```

# Task 6: Useful gh Tricks
- Explore and try these — add the ones you find useful to your git-commands.md:

- gh api — make raw GitHub API calls from the terminal
- gh gist — create and manage GitHub Gists
- gh release — create and manage releases
- gh alias — create shortcuts for commands you use often
- gh search repos — search GitHub repos from the terminal

```bash
to learn
```






