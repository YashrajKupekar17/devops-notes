# Lecture 5 – Git & GitHub (Day 1)

## 1. Why Git Exists (The Problem)

Before Git, developers shared code via emails like:
`app_final_v3_really_final_final.py`

Problems:

* No clear latest version
* One developer overwrote another’s work
* No history, no rollback

**Solution:** Version Control System (VCS)

---

## 2. What is SCM (Source Code Management)?

SCM helps teams **track, manage, and collaborate** on source code safely.

### Types of SCM

| Type                 | Where Code Lives              | Examples | Notes                   |
| -------------------- | ----------------------------- | -------- | ----------------------- |
| Local                | Single machine                | RCS      | No collaboration        |
| Remote (Centralized) | Central server                | SVN      | Network dependent       |
| Distributed          | Every developer has full copy | Git      | Offline + collaboration |

**Why Git is powerful:**

* Full history on every machine
* Works offline
* Each clone is a backup

---

## 3. Git vs GitHub

* **Git** → Version control tool (local)
* **GitHub** → Hosting & collaboration platform for Git repositories

---

## 4. Installing Git

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git -y
git --version
```

### Linux (RHEL/CentOS)

```bash
sudo yum update
sudo yum install git
git --version
```

---

## 5. Git Configuration (Identity)

Every commit needs an identity.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global core.editor "vim"
```

Check config:

```bash
git config --list
git config --global user.name
```

---

## 6. SSH Setup (Passwordless GitHub Access)

```bash
ssh-keygen -t rsa -b 4096 -C "email"
```

Add public key to GitHub → Settings → SSH Keys

---

## 7. Creating a Repository

```bash
mkdir demo
cd demo
git init
```

`.git/` directory stores:

* Commits
* Branches
* Objects
* Metadata

---

## 8. The Four Areas of Git

| Area         | Also Called | Purpose        |
| ------------ | ----------- | -------------- |
| Working Tree | Workspace   | Edit files     |
| Staging Area | Index       | Prepare commit |
| Local Repo   | .git        | Store commits  |
| Remote Repo  | origin      | Share code     |

Flow:

```
Working → Staging → Local Repo → Remote Repo
```

---

## 9. Basic Workflow

```bash
touch Abc.txt Xyz.txt
git status
git add Abc.txt
git commit -m "First commit"
```

Till commit → **No internet required**

---

## 10. Connecting to GitHub

```bash
git remote add origin git@github.com:user/repo.git
git push -u origin main
```

---

## 11. Viewing Changes & History

```bash
git status
git diff            # unstaged changes
git diff --staged   # staged changes
git log --oneline --graph --all
git show <commit>
```

---

## 12. Branching & Collaboration

```bash
git branch
git switch -c feature/x
git merge feature/x
git rebase main
```

---

## 13. Stash, Undo & Recovery

```bash
git stash
git stash pop
git revert <commit>
git reset --hard HEAD~1
git reflog
```

---

## 14. Git Best Practices

* Commit small logical changes
* Write meaningful commit messages
* Use feature branches
* Avoid force-push on shared branches

---