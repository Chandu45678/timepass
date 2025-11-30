# Experiment–2: Exploring Git Local and Remote Commands on a Multi-Folder Project

## Aim
To explore and execute complete Git local and remote commands on a multi-folder project including repository initialization, staging, committing, pushing, branching, merging, conflict resolution, stashing, remote tracking, branch deletion, and real-time collaboration.

## Software / Tools Required
- Git
- GitHub account with a private repository
- Git Bash / Terminal
- Code editor (VS Code / Notepad++ / etc.)
- A sample multi-folder project (e.g., src/, assets/, docs/)

---

## Step-by-Step Procedure

### 🔹 Step 1 — Create & Initialize Repository Locally
```bash
git init
git status
Step 2 — Add GitHub Repository as Remote
git remote add origin https://github.com/<username>/<repo>.git
git remote -v
Step 3 — Stage & Commit Files
git add .
git commit -m "Initial commit"
Step 4 — Push Project to GitHub
git push -u origin main
Detailed Git Commands Practised
🔹 Configuration Commands
git version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
git init
git clone <repo-url>
git status
git add .               # add all files
git add <filename>      # add one file
git commit -m "message"
git reset HEAD <file>          # unstage without removing edits
git restore <file>             # discard un-staged edits
git restore --staged <file>    # unstage file (equivalent to reset HEAD)
git reset --hard               # reset working directory to last commit
git log
git log --oneline --graph --decorate --all
git diff
git blame <file>
git branch
git branch <branch-name>
git checkout <branch-name>
git checkout -b <branch-name>
git checkout main
git merge <branch-name>
git merge --abort
# open conflicted file and edit lines between:
<<<<<<< HEAD
=======          
>>>>>>>
git add <file>
git commit -m "Resolve merge conflict"
git stash
git stash list
git stash pop
git branch -d <branch>    # delete merged branch
git branch -D <branch>    # force delete (even if not merged)
Full Remote Git Commands
🔹 Remote Repo Operationsgit remote -v
git remote add origin <url>
git remote remove origin
git remote rename origin github
git remote set-url origin <new-url>
Fetch / Pull / Push
git fetch origin
git pull origin main
git pull --rebase origin main
git push origin main
git push -u origin main     # set upstream tracking
git push origin <branch>
git fetch -p                # prune removed remote refs

🔹 Remote Branch Management
git branch -r
git fetch origin <branch>
git push origin --delete <branch>

Real-World Full Command Workflow (Tested Sequence)
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main

git checkout -b feature/login
# edit files
git add .
git commit -m "Add login module"
git push origin feature/login

git checkout main
git pull origin main
git merge feature/login

# If conflict occurs:
# edit conflicted file → remove conflict markers → keep correct lines
git add .
git commit -m "Resolve merge conflict"

git stash
git stash pop

git branch -d feature/login
git fetch origin
git pull origin main
git push origin main
git push origin --delete old-branch

Commands with Sample Output (O3 format)
git init

Initialized empty Git repository in C:/Movie/.git/

git remote -v

origin  https://github.com/<username>/<repo>.git (fetch)
origin  https://github.com/<username>/<repo>.git (push)

git push -u origin main

Branch 'main' set up to track remote branch 'main' from 'origin'.

git merge feature/login

CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and commit the result.

git stash pop

Applied stash and dropped the stash entry

git branch -d feature/login

Deleted branch feature/login (was 2ac1d4f).

git push origin --delete feature-ui

 - [deleted]  feature-ui