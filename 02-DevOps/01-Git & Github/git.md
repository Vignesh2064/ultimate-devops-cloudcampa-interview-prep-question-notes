### 🧩 **Basic Git Interview Questions and Answers**

#### 1. **What is Git?**

**Answer:** Git is a distributed version control system used to track changes in source code during software development. It allows multiple developers to work on the same codebase simultaneously.

---

#### 2. **What’s the difference between Git and GitHub?**

**Answer:**

* Git: A version control system installed locally to track code changes.
* GitHub: A cloud-based hosting service for Git repositories that allows collaboration.

---

#### 3. **What is a Git repository?**

**Answer:** A repository is a directory or storage space where your project files and version history are stored. It can be local or remote (e.g., on GitHub).

---

#### 4. **How do you initialize a Git repo?**

```bash
git init
```

Initializes a new Git repository in the current directory.

---

#### 5. **What is the difference between `git add` and `git commit`?**

* `git add`: Stages changes to be committed.
* `git commit`: Records the staged changes permanently in the repository.

---

#### 6. **How to check the current status of your Git repo?**

```bash
git status
```

---

#### 7. **How to view commit history?**

```bash
git log
```

---

#### 8. **What does `git clone` do?**

**Answer:** It copies a remote repository to your local machine.

---

#### 9. **How to create a new branch?**

```bash
git branch feature-x
```

---

#### 10. **How to switch branches?**

```bash
git checkout feature-x
```

---

### 🧪 **Intermediate Git Interview Questions and Answers**

#### 11. **What is the difference between `git pull` and `git fetch`?**

* `git pull`: Fetches and merges changes from remote.
* `git fetch`: Only fetches changes, does not merge.

---

#### 12. **What is a merge conflict?**

**Answer:** It occurs when two branches have changes in the same part of the file and Git doesn’t know which version to keep.

---

#### 13. **How do you resolve a merge conflict?**

* Open the conflicting file
* Decide what to keep/remove
* Mark it as resolved:

```bash
git add <filename>
git commit
```

---

#### 14. **How do you undo the last commit?**

```bash
git reset --soft HEAD~1    # Keep changes
git reset --hard HEAD~1    # Remove changes
```

---

#### 15. **What is the staging area in Git?**

**Answer:** It's where changes are placed using `git add` before they are committed.

---

#### 16. **How do you stash changes?**

```bash
git stash
```

Temporarily shelves changes for later use.

---

#### 17. **How to apply a stashed change?**

```bash
git stash pop
```

---

#### 18. **How do you delete a branch?**

```bash
git branch -d feature-x
```

---

#### 19. **How to remove untracked files?**

```bash
git clean -f
```

---

#### 20. **How to ignore files in Git?**

**Answer:** Use a `.gitignore` file to list the files or directories to be ignored.

---

### 🔧 **Advanced Git Interview Questions and Answers**

#### 21. **What is Git Rebase and how is it different from Merge?**

**Answer:**

* `git rebase`: Moves or replays your changes on top of another branch (linear history).
* `git merge`: Combines histories from different branches (may create merge commits).

---

#### 22. **What is a detached HEAD in Git?**

**Answer:** It means you are not on a branch, but on a specific commit. Changes made won't belong to any branch unless explicitly assigned.

---

#### 23. **How do you cherry-pick a commit from another branch?**

```bash
git cherry-pick <commit-hash>
```

---

#### 24. **What is `.gitkeep`?**

**Answer:** A conventionally named empty file used to ensure empty folders are tracked by Git.

---

#### 25. **How to revert a pushed commit?**

```bash
git revert <commit-hash>
git push origin main
```

---

#### 26. **How to see a visual graph of commits?**

```bash
git log --oneline --graph --all
```

---

#### 27. **What is the difference between `reset`, `revert`, and `checkout`?**

* `reset`: Moves HEAD and can modify history.
* `revert`: Creates a new commit to undo changes.
* `checkout`: Switches branches or files.

---

#### 28. **How do you squash commits?**

```bash
git rebase -i HEAD~3
```

---

#### 29. **What is a `git tag`?**

**Answer:** Tags are used to mark specific points in history as important (e.g., v1.0, release).

---

#### 30. **How to track a remote branch locally?**

```bash
git checkout --track origin/feature-x
```

---

### 🔍 **Scenario-Based Git Interview Questions and Answers**

#### 31. **Scenario: You committed secrets to Git. What should you do?**

**Answer:**

* Remove secrets from the code.
* Use `git filter-branch` or `BFG Repo-Cleaner` to purge history.
* Force push the cleaned history:

```bash
git push origin --force --all
```

---

#### 32. **Scenario: Your teammate pushed broken code to `main`. What do you do?**

**Answer:**

* Revert the specific commit:

```bash
git revert <commit-hash>
```

* Or use branch protection to avoid direct push next time.

---

#### 33. **Scenario: You need to test a fix without committing your current work.**

**Answer:**

* Use `git stash` to save your work:

```bash
git stash
git checkout fix-branch
```

---

#### 34. **Scenario: You want to keep your history clean before PR.**

**Answer:**

* Use interactive rebase to squash/fixup commits.

```bash
git rebase -i HEAD~n
```

---

#### 35. **Scenario: You accidentally deleted your local branch. How to recover?**

**Answer:**

* If not yet garbage collected:

```bash
git reflog
git checkout -b branch-name <commit-id>
```

---

#### 36. **Scenario: Two developers worked on same file and now merge conflict arises. How to resolve?**

**Answer:**

* Pull and merge, then manually edit the file.
* Stage and commit.

---

#### 37. **Scenario: How to ensure everyone uses the same hooks?**

**Answer:**

* Store hooks in the repo and use symlinks or tools like **Husky** for automation.

---

#### 38. **Scenario: Someone force pushed and broke history. What do you do?**

**Answer:**

* Use `reflog` to find previous commits.
* Create a new branch and recover.

---

#### 39. **Scenario: You want to share part of a repo without the entire codebase.**

**Answer:**

* Use `git subtree` or `git filter-repo` to extract and share a directory as a new repo.

---

#### 40. **Scenario: Your commit email is incorrect. How to change it retroactively?**

```bash
git rebase -i HEAD~n
# Amend each commit or use filter-branch:
git filter-branch --commit-filter '
if [ "$GIT_COMMITTER_EMAIL" = "wrong@example.com" ];
then
    GIT_COMMITTER_NAME="Correct Name";
    GIT_COMMITTER_EMAIL="correct@example.com";
    git commit-tree "$@";
else
    git commit-tree "$@";
fi' HEAD
```

---

## ✅ **Git Interview Questions and Answers (Including Hooks)**

> Covers: Basics → Advanced → Scenarios → Hooks

---

### 🧩 **Basic Git Questions**

Already covered in detail \[see previous message], but here are some hook-related entries to introduce the concept:

#### 🔹 11. **What are Git Hooks?**

**Answer:**
Git Hooks are scripts that run automatically at specific points in the Git lifecycle — for example, before a commit or after a push. They’re stored in the `.git/hooks` directory.

---

### 🧪 **Intermediate Questions (Hooks Included)**

#### 🔹 21. **What are common types of Git hooks?**

| Hook Name            | Trigger Time          | Purpose                               |
| -------------------- | --------------------- | ------------------------------------- |
| `pre-commit`         | Before commit         | Lint checks, run tests, format code   |
| `prepare-commit-msg` | Before message editor | Auto-add ticket number to commit msg  |
| `commit-msg`         | After msg written     | Validate commit message format        |
| `pre-push`           | Before pushing code   | Run tests, prevent push if failing    |
| `post-merge`         | After merge           | Rebuild dependencies or notify system |

---

#### 🔹 22. **Where are hooks stored?**

**Answer:** In every Git repository at:

```
.git/hooks/
```

These are local and not shared by default.

---

#### 🔹 23. **How to enable a hook?**

**Answer:** Remove the `.sample` extension from any hook and make it executable:

```bash
chmod +x .git/hooks/pre-commit
```

---

#### 🔹 24. **Can you share hooks across teams?**

**Answer:** Yes, but not directly through `.git/hooks`. Instead, use tools like:

* **Husky** (JavaScript-based projects)
* **lefthook** (language-agnostic)
* Include hook scripts in a versioned folder and symlink them.

---

### 🔧 **Advanced Git + Hooks Questions**

#### 🔹 31. **How can hooks be used in CI/CD pipelines?**

**Answer:** Hooks can run local pre-checks before pushing to CI, e.g., formatting or security scanning. In pipelines, custom hook scripts can be embedded in GitLab/GitHub CI to enforce policies before merges.

---

#### 🔹 32. **What is the difference between client-side and server-side hooks?**

| Type        | Location      | Examples                      |
| ----------- | ------------- | ----------------------------- |
| Client-side | `.git/hooks/` | `pre-commit`, `pre-push`      |
| Server-side | On Git server | `pre-receive`, `post-receive` |

**Example:** Server-side hooks reject bad pushes on GitHub Enterprise or GitLab.

---

#### 🔹 33. **Write a simple `pre-commit` hook to prevent commits with TODO comments**

```bash
#!/bin/bash
if grep -rnw 'TODO' .; then
  echo "❌ Commit blocked: TODOs found"
  exit 1
fi
```

---

#### 🔹 34. **How do you enforce commit message standards using hooks?**

Create a `commit-msg` hook:

```bash
#!/bin/sh
MSG=$(cat $1)
if ! echo "$MSG" | grep -qE "^(feat|fix|docs|refactor):"; then
  echo "❌ Invalid commit message. Use conventional format!"
  exit 1
fi
```

---

### 🧠 **Scenario-Based Git + Hooks Questions**

#### 🔹 41. **Scenario: You want to ensure every developer runs lint before committing.**

**Solution:**

* Create a `pre-commit` hook that runs `eslint` or a linter
* Share via Husky or symlinks in the repo

---

#### 🔹 42. **Scenario: You want to block pushes to `main` unless tests pass.**

**Solution:**
Use a `pre-push` hook:

```bash
#!/bin/bash
npm test
if [ $? -ne 0 ]; then
  echo "❌ Tests failed. Push rejected."
  exit 1
fi
```

---

#### 🔹 43. **Scenario: How do you enforce commit message policy across an organization?**

**Solution:**

* Use `commit-msg` hook locally (can be installed via Husky).
* Or use server-side hooks (e.g., GitHub Actions or GitLab push rules).

---

#### 🔹 44. **Scenario: How to keep all contributors using the same Git hooks?**

**Solution:**

1. Store hooks in `/hooks/` folder.
2. Add a setup script:

```bash
ln -s ../../hooks/pre-commit .git/hooks/pre-commit
```

3. Automate using Husky or Makefile.

---

#### 🔹 45. **Scenario: You want to auto-install Git hooks after cloning.**

**Solution:**
Add a `post-checkout` or install script in `package.json` or CI setup to run:

```bash
npm run setup-hooks
```

---

## 🧰 BONUS: Recommended Hook Tools

| Tool           | Description                        |
| -------------- | ---------------------------------- |
| **Husky**      | Popular tool to manage hooks in JS |
| **Lefthook**   | Language-agnostic, fast, CI-ready  |
| **Pre-commit** | Python-based hook manager          |
| **Overcommit** | Ruby-based, highly configurable    |

---

## 🚀 **Additional Git & GitHub Interview Questions You Should Know**

### 🔄 **Git Concepts and Collaboration**

#### 1. **What is a fork in GitHub?**

**Answer:**
A fork is a personal copy of someone else's repository on your GitHub account. You can make changes independently without affecting the original repo.

---

#### 2. **What’s the difference between fork and clone?**

| Operation | Scope        | Use Case                                |
| --------- | ------------ | --------------------------------------- |
| Fork      | GitHub-level | Copy repo to your GitHub to contribute  |
| Clone     | Local-level  | Copy repo to your machine to work on it |

---

#### 3. **How do you contribute to an open-source project on GitHub?**

**Steps:**

1. Fork the repository.
2. Clone your fork locally.
3. Create a new branch.
4. Make changes and commit.
5. Push the branch to your fork.
6. Create a **Pull Request (PR)** to the original repo.

---

#### 4. **What is a Pull Request (PR)?**

**Answer:**
A request to merge your code changes into another branch/repo (commonly `main`). It allows for code reviews, testing, and discussion before merging.

---

#### 5. **How do you handle code reviews via GitHub?**

* Request reviewers
* Use GitHub comments & suggestions
* Address feedback via new commits
* Approve/merge PR or request changes

---

### ⚠️ **Best Practices and Git Workflows**

#### 6. **What is GitFlow?**

**Answer:**
A branching model with specific roles:

* `main` – production-ready
* `develop` – ongoing development
* `feature/*`, `release/*`, `hotfix/*` – for organizing changes

---

#### 7. **What’s the difference between `main`, `develop`, and `feature` branches?**

| Branch  | Purpose                                |
| ------- | -------------------------------------- |
| main    | Stable, production code                |
| develop | Integration of features before release |
| feature | Work on specific tasks or stories      |

---

#### 8. **How do you revert a PR merge on GitHub?**

* Use **"Revert" button** on GitHub if available.
* Or locally:

```bash
git revert -m 1 <merge_commit_hash>
```

---

#### 9. **How do you squash commits in a PR before merging?**

* Use `git rebase -i HEAD~n` locally
* Or use **"Squash and merge"** button on GitHub

---

#### 10. **What are GitHub Actions?**

**Answer:**
CI/CD workflows directly integrated with your GitHub repo for automating tests, deployments, linting, etc.

---

### 🔐 **GitHub Permissions, Security, and Secrets**

#### 11. **How do you manage access to a GitHub repo?**

* Use **Collaborators** for personal repos
* Use **Teams & Roles** in GitHub Organizations
* Apply **branch protection rules**

---

#### 12. **What are branch protection rules in GitHub?**

**Answer:**
Settings that prevent:

* Force pushes
* Direct commits to `main`
* Merging without review/checks

Example: Require 1 reviewer and successful CI before merge.

---

#### 13. **How do you store secrets securely in GitHub?**

* Go to **Settings → Secrets and Variables**
* Use **GitHub Secrets** for workflows

```yaml
env:
  AWS_SECRET: ${{ secrets.AWS_SECRET }}
```

---

#### 14. **How do you enforce commit signing?**

**Answer:**

* Configure **GPG or SSH signing**
* Enforce via GitHub repo settings to accept signed commits only

---

#### 15. **How do you audit contributions and changes in GitHub?**

* Use **GitHub Insights**
* Review **commit history**, **PRs**, and **blame** for file authorship
* Enable **audit logs** for organizations

---

### 🛠️ **Other Advanced Git/GitHub Concepts**

#### 16. **What is a shallow clone in Git?**

```bash
git clone --depth=1 <repo-url>
```

**Answer:**
Clones only the latest commit. Useful for CI/CD pipelines for faster operations.

---

#### 17. **How do you rename a branch locally and remotely?**

```bash
git branch -m old-name new-name
git push origin :old-name new-name
git push origin -u new-name
```

---

#### 18. **What is `git bisect`?**

**Answer:**
Binary search to find the commit that introduced a bug:

```bash
git bisect start
git bisect bad
git bisect good <commit>
```

---

#### 19. **What is GitHub Copilot and how can it help?**

**Answer:**
GitHub Copilot is an AI-powered code assistant that suggests code based on context. It can speed up development, write tests, and generate boilerplate.

---

#### 20. **What is GitHub CLI?**

**Answer:**
`gh` is the official GitHub command-line interface. Examples:

```bash
gh repo clone
gh pr create
gh issue list
```

---
