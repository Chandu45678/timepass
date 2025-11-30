# Experiment–3: Collaborative Coding Using Git

## Aim
To perform collaborative software development using Git and GitHub by creating organizations, sharing repositories, working with branches, creating pull requests, resolving merge conflicts, and applying patches between collaborators.

## Software / Tools Required
- Git installed on the system
- GitHub account
- Minimum two collaborators
- Browser and Git Bash / Terminal
- Code editor (VS Code, Notepad++, Nano, etc.)

---

## Step-by-Step Procedure

### 🔹 Step 1 — Create a GitHub Organization (Collaborator 1)
1. Login to GitHub → Profile → **Your organizations → New organization**
2. Select **Free plan**
3. Enter **Organization name**, email, and verify account
4. Click **Next**
5. Add collaborators (GitHub usernames / emails)
6. Complete setup
7. Configure permissions:
   - Organization → **Settings → Member privileges**
   - **Base permissions → Write**
   - **Projects base permissions → Write**

### 🔹 Step 2 — Create Shared Repository Inside Organization (Collaborator 1)
1. Go to Organization → **New repository**
2. Set visibility to **Private**
3. Click **Create repository**

### 🔹 Step 3 — Access Shared Repository (Collaborator 2)

#### Configure Git
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
Clone the shared repo
git clone https://github.com/<org-name>/<repo>.git
cd <repo>

🔹 Step 4 — Work on Branches for Collaborative Coding
Collaborator 2 — Create feature branch
git checkout -b feature/login

Modify files → Stage → Commit
git add .
git commit -m "Add login functionality"

Push branch to shared repository
git push origin feature/login

Create Pull Request

Open GitHub → Repository

Click Compare & pull request

Add title + description → Create pull request

Collaborator 1 — Merge PR

Open Pull Requests tab

Review changes → add comments if needed

Click Merge pull request → Confirm merge

Fork Workflow (If Working on Public Projects)
🔹 Step 5 — Fork a Public Repository (Collaborator 2)

Go to the target GitHub repo

Click Fork

New fork appears at: https://github.com/<your-username>/<repo>

Clone your fork
git clone https://github.com/<your-username>/<repo>.git
cd <repo>

Create branch + modify + commit + push
git checkout -b bugfix/ui
git add .
git commit -m "Fix UI alignment"
git push origin bugfix/ui

Raise PR

Open fork → Pull requests → New pull request

Submit to the original repository

Merge Conflict Resolution
🔹 Step 6 — Create conflict scenario

Collaborator 1 and Collaborator 2 modify the same line in README.md in different branches.

🔹 Step 7 — Attempt merge (conflict happens)
git checkout main
git merge feature/ui


💥 Output

CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and commit the result.

🔹 Step 8 — Fix conflict manually

Inside file you will see:

<<<<<<< HEAD
Line by Collaborator 1
=======
Line by Collaborator 2
>>>>>>> feature/ui


Resolve it by keeping appropriate content and remove markers.

🔹 Step 9 — Stage & commit conflict resolution
git add README.md
git commit -m "Resolve merge conflict in README.md"
git push origin main

Patch-Based Collaboration
🔹 Step 10 — Create Patch (Collaborator 2)
git log --oneline -1
# copy commit hash e.g., abc1234

git format-patch -1 abc1234


Output:

0001-Fix-UI-alignment.patch


Send this .patch file to the repository owner.

🔹 Step 11 — Apply Patch (Collaborator 1)
git am 0001-Fix-UI-alignment.patch


Output:

Applying: Fix UI alignment


Confirm changes:

git status
git log --oneline

Full Collaboration Command Workflow (Sequential Overview)
git config --global user.name "User"
git config --global user.email "user@example.com"

git clone https://github.com/<org-name>/<repo>.git
cd <repo>

git checkout -b feature/login
# edit code
git add .
git commit -m "Add login module"
git push origin feature/login
# open PR on GitHub

git checkout main
git pull origin main
git merge feature/login

# if conflict
# edit file → remove conflict markers
git add .
git commit -m "Resolve conflict in README.md"

git branch -d feature/login
git push origin main

Commands with Sample Output (O3 Format)
git clone https://github.com/<org-name>/<repo>.git

Cloning into 'repo'...
remote: Enumerating objects...
Receiving objects: 100%

git push origin feature/login

To https://github.com/<org-name>/<repo>.git
 * [new branch]      feature/login → feature/login

git merge feature/login

Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and commit the result.

git am 0001-Fix-UI-alignment.patch

Applying: Fix UI alignment

git branch -d feature/login

Deleted branch feature/login (was 63d1af4).
