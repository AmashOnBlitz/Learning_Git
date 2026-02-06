# The Complete Git Guide
## From Absolute Beginner to Advanced User

**A Comprehensive, Printable Reference for Understanding Git**

Version 1.0 | February 2026

---

## Table of Contents

### Part 1: Foundation (Beginner)
1. **Introduction: What is Git?**
   - What Git Is
   - What Git Is NOT
   - Why Git Exists
   - Git vs GitHub (and GitLab, Bitbucket)

2. **Core Concepts: Mental Models**
   - The Repository: Your Project's Time Machine
   - Commits: Snapshots, Not Diffs
   - Branches: Parallel Universes
   - HEAD: Your Current Location
   - The Three States of Files
   - The Staging Area: Why It Exists

3. **Getting Started**
   - Installing Git
   - Initial Configuration
   - Your First Repository

4. **The Basic Workflow**
   - Understanding the Daily Cycle
   - git init
   - git clone
   - git status
   - git add
   - git commit
   - git log
   - Complete Beginner Workflow

### Part 2: Building Skills (Intermediate)

5. **Branches in Depth**
   - What Branches Really Are
   - Creating and Switching Branches
   - git checkout vs git switch
   - Branching from Branches
   - Branch Naming Conventions
   - Deleting Branches

6. **Viewing History and Changes**
   - git log (All the Useful Flags)
   - git diff (All Variants)
   - Comparing Branches
   - Finding Specific Changes

7. **Ignoring Files**
   - What .gitignore Does
   - Pattern Rules Explained
   - Common .gitignore Templates
   - When .gitignore Doesn't Work

8. **Stashing: Temporary Storage**
   - What Stash Is
   - When to Use It
   - Stash Commands
   - Common Stash Workflows

9. **Merging: Bringing Branches Together**
   - Fast-Forward Merge
   - Three-Way Merge
   - Merge Conflicts: Why They Happen
   - How to Resolve Conflicts
   - Merge Best Practices

10. **Working with Remote Repositories**
    - Understanding Remotes
    - git remote
    - git fetch vs git pull
    - git push
    - Pull Requests Explained

11. **Safe Workflows**
    - Solo Developer Workflow
    - Team Workflow
    - Feature Branch Workflow

### Part 3: Advanced Techniques

12. **Rewriting History**
    - git reset (soft, mixed, hard)
    - git revert
    - When to Use Which

13. **Rebasing**
    - What Rebase Does
    - Interactive Rebase
    - Rebase vs Merge: The Decision Table
    - The Golden Rule of Rebase
    - Practical Rebase Workflows

14. **Advanced Operations**
    - git cherry-pick
    - Detached HEAD State
    - git reflog: The Safety Net
    - Recovering Lost Commits

15. **Clean History Principles**
    - Why Clean History Matters
    - Squashing Commits
    - Commit Message Best Practices
    - Amending Commits

### Part 4: Quick Reference

16. **Cheat Sheets**
    - Daily Commands
    - Branching Workflow
    - Conflict Resolution Steps
    - Emergency Recovery
    - Dangerous Commands List

17. **Real-World Workflows**
    - Experiment → Fail → Discard
    - Experiment → Success → Merge
    - Multiple Experiments
    - Hotfix Workflow
    - Release Management

18. **Common Mistakes and Fixes**
    - Committed to Wrong Branch
    - Need to Undo Last Commit
    - Accidentally Deleted a Branch
    - Pushed Sensitive Data
    - Merge Conflicts Everywhere

---

# Part 1: Foundation (Beginner)

## 1. Introduction: What is Git?

### What Git Is

Git is a **version control system**. Think of it as a sophisticated "save game" system for your code and files, but with superpowers:

- **Time travel**: You can go back to any previous version of your files
- **Parallel universes**: You can work on multiple versions simultaneously
- **Collaboration**: Multiple people can work on the same files without chaos
- **Safety net**: You can experiment freely knowing you can always undo

**The Simple Analogy**: 

Imagine writing a book:
- Without Git: You have "MyNovel.doc", "MyNovel_v2.doc", "MyNovel_FINAL.doc", "MyNovel_FINAL_FOR_REAL.doc"
- With Git: You have one "MyNovel.doc" file, but Git remembers every version you've saved, with notes about what you changed and why

### What Git Is NOT

Let's clear up common misconceptions:

❌ **Git is NOT GitHub**
- Git = The version control tool (software on your computer)
- GitHub = A website that hosts Git repositories (like Dropbox for Git)

❌ **Git is NOT a backup system**
- It's designed for version control, not file storage
- Though it does keep history, that's not its primary purpose

❌ **Git is NOT just for code**
- You can version control any text files
- Common uses: documentation, configuration files, books, essays
- Less ideal for: large binary files, videos, images (though possible)

❌ **Git is NOT automatic**
- You decide when to save versions (commits)
- You decide what to save
- You decide when to sync with others

### Why Git Exists

Before Git, developers had problems:

**Problem 1: "It worked yesterday!"**
- Solution: Git lets you see exactly what changed and go back

**Problem 2: "Who broke the code?"**
- Solution: Git tracks who changed what and when

**Problem 3: "I want to try this risky idea..."**
- Solution: Git lets you experiment in branches without affecting the main code

**Problem 4: "How do we all work on this together?"**
- Solution: Git manages multiple people editing the same files

### Git vs GitHub (and GitLab, Bitbucket)

This confuses EVERYONE at first, so let's be crystal clear:

```
┌─────────────────────────────────────────┐
│  YOUR COMPUTER                          │
│                                         │
│  ┌────────────────┐                    │
│  │  Git (local)   │                    │
│  │  - Tracks      │                    │
│  │    changes     │                    │
│  │  - Stores      │                    │
│  │    history     │                    │
│  │  - Creates     │                    │
│  │    branches    │                    │
│  └────────────────┘                    │
│                                         │
└─────────────────────────────────────────┘
           │
           │ git push / git pull
           ▼
┌─────────────────────────────────────────┐
│  THE INTERNET                           │
│                                         │
│  ┌────────────────┐                    │
│  │  GitHub        │  ← Website/Service │
│  │  - Stores a    │                    │
│  │    copy online │                    │
│  │  - Nice UI     │                    │
│  │  - Team tools  │                    │
│  │  - Pull        │                    │
│  │    Requests    │                    │
│  └────────────────┘                    │
│                                         │
└─────────────────────────────────────────┘
```

**Git**: The engine in your car (runs locally on your machine)
**GitHub**: A parking garage for your car (stores it online, adds extra features)

**Alternatives to GitHub**:
- **GitLab**: Similar to GitHub, can self-host
- **Bitbucket**: Atlassian's version
- **Your own server**: You can host Git anywhere

**Key Insight**: You can use Git without ever using GitHub. GitHub is just a popular place to store and share repositories.

---

## 2. Core Concepts: Mental Models

### The Repository: Your Project's Time Machine

A **repository** (or "repo") is a folder that Git is tracking.

```
my-project/              ← Your project folder
├── .git/                ← Git's magic folder (DON'T TOUCH)
│   └── (Git's internal files)
├── index.html
├── style.css
└── script.js
```

The `.git` folder is where Git stores:
- All the history
- All the branches
- All the configuration

**Mental Model**: Think of `.git` as a hidden photo album that automatically takes snapshots of your entire project folder whenever you tell it to.

**Important**: If you delete the `.git` folder, you lose all Git history (but your current files remain). The project is no longer a Git repository.

### Commits: Snapshots, Not Diffs

A **commit** is a snapshot of your entire project at a specific moment in time.

**Wrong Mental Model** ❌: "Commits are the changes I made"

**Correct Mental Model** ✅: "Commits are complete snapshots, and Git is smart enough to only store the changes"

```
Commit A (Monday)          Commit B (Tuesday)         Commit C (Wednesday)
┌──────────────┐          ┌──────────────┐          ┌──────────────┐
│ index.html   │          │ index.html   │          │ index.html   │
│ style.css    │   →      │ style.css    │   →      │ style.css    │
│ script.js    │          │ script.js    │          │ script.js    │
└──────────────┘          │ about.html   │          │ about.html   │
                          └──────────────┘          │ contact.html │
                                                    └──────────────┘
```

Each commit includes:
- The snapshot of all files
- A unique ID (hash): `a3f5e2c...`
- Author name and email
- Timestamp
- Commit message (your note about what changed)
- Pointer to the previous commit (parent)

**The Chain of Commits**:

```
(oldest) ← commit1 ← commit2 ← commit3 ← commit4 (newest)
```

This chain IS your project's history.

### Branches: Parallel Universes

A **branch** is simply a movable label pointing to a commit.

**Terrible Analogy**: Branches are copies of your code ❌

**Better Analogy**: Branches are alternative storylines in a choose-your-own-adventure book ✅

```
                    ┌─ commit4 ← commit5 (experiment branch)
                    │
commit1 ← commit2 ← commit3 ← commit6 (main branch)
```

**What Actually Happens**:
1. You create a branch: Git creates a new label
2. You switch to that branch: Git changes what you see
3. You make commits: Only that branch's label moves forward
4. Switching branches: Git swaps out files to match that branch

**The Magic**: Git doesn't duplicate files. It just changes what you see based on which branch you're on.

**Default Branch**: Usually called `main` (or `master` in older repos)

### HEAD: Your Current Location

**HEAD** is a pointer to "where you are right now" in the Git history.

```
                    experiment
                         ↓
commit1 ← commit2 ← commit3 ← commit4
                              ↑
                            HEAD
```

When you see `HEAD` in commands:
- It means "the commit I'm currently looking at"
- Usually points to the tip of a branch
- Sometimes points directly to a commit (detached HEAD - we'll cover later)

**Simple rule**: HEAD = "You Are Here" marker

### The Three States of Files

Every file in your Git repository is in one of three states:

```
┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│   MODIFIED   │  →   │    STAGED    │  →   │  COMMITTED   │
│              │      │              │      │              │
│ You changed  │      │ Ready to be  │      │ Safely       │
│ the file     │      │ committed    │      │ stored in    │
│              │      │ (in staging  │      │ .git         │
│              │      │ area)        │      │              │
└──────────────┘      └──────────────┘      └──────────────┘
```

**Modified**: You've changed the file, but haven't told Git to save it

**Staged**: You've told Git "include this in the next snapshot"

**Committed**: The changes are permanently stored in Git's database

**Why This Matters**: Understanding these states prevents confusion about why Git "isn't saving my changes"

### The Staging Area: Why It Exists

The **staging area** (also called the "index") is the middle ground between your working files and the Git repository.

**Confusing Question**: "Why can't I just commit files directly?"

**Answer**: The staging area lets you craft perfect commits.

**Example Scenario**:

You've been working and changed 3 files:
- `bug-fix.js` (fixed a bug)
- `new-feature.js` (half-finished feature)
- `typo-in-readme.md` (fixed a typo)

You want to commit the bug fix NOW, but the feature isn't ready.

```
Working Directory          Staging Area           Repository
┌──────────────┐          ┌──────────────┐       ┌──────────────┐
│ bug-fix.js   │  add →   │ bug-fix.js   │ commit│ bug-fix.js   │
│ (modified)   │          │ (staged)     │   →   │ (committed)  │
├──────────────┤          └──────────────┘       └──────────────┘
│ feature.js   │
│ (modified)   │  ← NOT ADDED, won't be committed
├──────────────┤
│ readme.md    │
│ (modified)   │
└──────────────┘
```

**The Power**: You can stage only `bug-fix.js`, commit it, and leave the other files for later.

**Mental Model**: The staging area is your "shopping cart" before checkout. You can add/remove items before finalizing the purchase.

---

## 3. Getting Started

### Installing Git

**Windows**:
1. Download from https://git-scm.com
2. Run installer (accept defaults)
3. Use "Git Bash" terminal

**Mac**:
```bash
# Using Homebrew (recommended)
brew install git

# Or download from git-scm.com
```

**Linux** (Ubuntu/Debian):
```bash
sudo apt-get update
sudo apt-get install git
```

**Verify Installation**:
```bash
git --version
```

Should show something like: `git version 2.40.0`

### Initial Configuration

**IMPORTANT**: Do this before your first commit.

Git needs to know who you are (for the commit author field):

```bash
# Set your name (use your real name)
git config --global user.name "Jane Smith"

# Set your email (use the same email as your GitHub account if you use GitHub)
git config --global user.email "jane@example.com"
```

**Optional but Recommended**:

```bash
# Set default branch name to 'main' (modern standard)
git config --global init.defaultBranch main

# Better command line colors
git config --global color.ui auto

# Set your preferred text editor for commit messages
git config --global core.editor "nano"  # or "vim", "code --wait", etc.
```

**View Your Configuration**:
```bash
git config --list
```

**What `--global` Means**: These settings apply to all repositories on your computer. You can override them per-repository by omitting `--global`.

### Your First Repository

**Two Ways to Get a Repository**:

#### Option 1: Start a New Project

```bash
# Create a project folder
mkdir my-project
cd my-project

# Initialize Git
git init
```

**What Happened**: Git created a `.git` folder in your directory.

```bash
# Verify
ls -la
# You should see .git/ in the output
```

#### Option 2: Clone an Existing Project

```bash
# Clone from GitHub (or any Git server)
git clone https://github.com/username/repository.git

# This creates a folder named 'repository' with the project inside
cd repository
```

**What Happened**: Git downloaded the entire project history and created a local copy.

**Your First Commit**:

```bash
# Create a file
echo "# My Project" > README.md

# Check status
git status
# Shows: README.md is untracked

# Add to staging area
git add README.md

# Check status again
git status
# Shows: README.md is staged

# Commit
git commit -m "Initial commit: Add README"

# Check history
git log
```

**Congratulations!** You've created your first Git repository and made your first commit.

---

## 4. The Basic Workflow

### Understanding the Daily Cycle

The typical Git workflow looks like this:

```
1. Make changes to files
         ↓
2. Check what changed (git status)
         ↓
3. Stage the changes (git add)
         ↓
4. Commit the changes (git commit)
         ↓
5. (Optional) Push to remote (git push)
         ↓
   (Repeat)
```

### git init

**What It Does**: Turns a regular folder into a Git repository

**When to Use**: Starting a brand new project

**Syntax**:
```bash
git init
```

**What Happens**:
- Creates `.git` directory
- Sets up initial Git structure
- Does NOT create any commits yet

**Example**:
```bash
mkdir my-website
cd my-website
git init
# Initialized empty Git repository in /path/to/my-website/.git/
```

**When NOT to Use**:
- Inside an existing Git repository (Git repos shouldn't be nested)
- If you're cloning someone else's project (use `git clone` instead)

**Common Mistake**: Initializing Git in your home directory or root directory. NEVER do this:
```bash
cd ~
git init  # ❌ DON'T DO THIS
```

### git clone

**What It Does**: Downloads a complete copy of a repository from somewhere else

**When to Use**: Starting work on an existing project

**Syntax**:
```bash
git clone  [folder-name]
```

**Parameters**:
- `<url>`: The repository address
  - HTTPS: `https://github.com/user/repo.git`
  - SSH: `git@github.com:user/repo.git`
  - Local: `/path/to/repo` or `file:///path/to/repo`
- `[folder-name]`: Optional; custom name for the folder

**Examples**:
```bash
# Basic clone
git clone https://github.com/user/awesome-project.git
# Creates folder 'awesome-project'

# Clone with custom folder name
git clone https://github.com/user/awesome-project.git my-version
# Creates folder 'my-version'

# Clone a specific branch
git clone -b develop https://github.com/user/repo.git
```

**What Gets Cloned**:
- All commits
- All branches
- All tags
- The entire history
- .gitignore and other config files

**What Doesn't Get Cloned**:
- Unstaged/uncommitted changes (obviously)
- Your local Git config (you'll need to set user.name/email)

**Common Mistake**: Cloning inside an existing repository
```bash
cd my-project
git clone https://github.com/some/other-project.git  # ❌ Creates nested repo
```

### git status

**What It Does**: Shows the current state of your working directory and staging area

**When to Use**: All the time! Before and after every operation

**Syntax**:
```bash
git status
```

**What It Shows**:

```bash
On branch main                    ← Which branch you're on
Your branch is up to date with 'origin/main'.

Changes to be committed:          ← Staged files (green)
  (use "git restore --staged ..." to unstage)
        new file:   index.html
        modified:   style.css

Changes not staged for commit:    ← Modified but not staged (red)
  (use "git add ..." to update what will be committed)
  (use "git restore ..." to discard changes)
        modified:   script.js

Untracked files:                  ← New files Git doesn't know about
  (use "git add ..." to include in what will be committed)
        notes.txt
```

**Color Coding** (in terminal):
- **Green**: Staged (will be in next commit)
- **Red**: Modified or untracked (won't be in next commit)

**Short Format**:
```bash
git status -s
# Output:
# M  style.css      ← Modified and staged
#  M script.js      ← Modified but not staged
# ?? notes.txt      ← Untracked
# A  index.html     ← Added (new file staged)
```

**When NOT to Use**: Never! Use it constantly!

**Pro Tip**: Make `git status` a habit. Type it before and after every Git command while learning.

### git add

**What It Does**: Moves changes from "modified" to "staged" (adds to staging area)

**When to Use**: Before committing, to select which changes to include

**Syntax**:
```bash
git add 
```

**Common Patterns**:

```bash
# Add a specific file
git add index.html

# Add multiple specific files
git add index.html style.css script.js

# Add all files in current directory
git add .

# Add all files in the repository
git add -A
# or
git add --all

# Add all files of a certain type
git add *.js

# Add parts of a file interactively (advanced)
git add -p
```

**What Each Variant Does**:

| Command | What It Adds |
|---------|--------------|
| `git add <file>` | Specific file |
| `git add .` | All changes in current directory and subdirectories |
| `git add -A` | All changes anywhere in repository |
| `git add -u` | Only modified/deleted files (not new files) |
| `git add -p` | Interactive mode - choose chunks to stage |

**Visual Example**:

```bash
# Before
$ git status
  modified: file1.txt
  modified: file2.txt
  new file: file3.txt

# Add one file
$ git add file1.txt

# After
$ git status
Changes to be committed:
  modified: file1.txt    ← Staged

Changes not staged:
  modified: file2.txt    ← Not staged
  new file: file3.txt
```

**Common Mistakes**:

❌ **Forgetting to add files before commit**:
```bash
# You changed file.txt
git commit -m "Update file"  # ❌ Nothing happens!
# Correct:
git add file.txt
git commit -m "Update file"  # ✅
```

❌ **Adding files you don't want to commit**:
```bash
git add .  # ❌ Adds EVERYTHING, including temp files

# Better: Be selective or use .gitignore
git add src/
```

**When NOT to Use**:
- Don't add sensitive data (passwords, API keys)
- Don't add generated files (build outputs)
- Don't add large binary files unnecessarily

### git commit

**What It Does**: Creates a snapshot of staged changes and saves it to Git history

**When to Use**: After staging changes that represent a logical unit of work

**Syntax**:
```bash
git commit -m "Your commit message"
```

**Common Patterns**:

```bash
# Basic commit with message
git commit -m "Add user authentication"

# Multi-line commit message (opens editor)
git commit
# Then type message in editor, save and close

# Commit and add all tracked files in one step
git commit -am "Fix typo in README"
# Same as: git add -u && git commit -m "..."

# Amend the previous commit (advanced)
git commit --amend
```

**Parameters Explained**:

| Flag | What It Does | When to Use |
|------|--------------|-------------|
| `-m "message"` | Inline commit message | Always (unless multi-line) |
| `-a` | Auto-stage modified files | Quick commits of tracked files |
| `--amend` | Modify last commit | Forgot to include a file or fix message |
| `-v` | Show diff in editor | See changes while writing message |
| `--no-edit` | Keep existing message | Use with --amend |

**Commit Message Best Practices**:

```bash
# ✅ GOOD MESSAGES
git commit -m "Add login button to header"
git commit -m "Fix crash when username is empty"
git commit -m "Update README with installation steps"

# ❌ BAD MESSAGES
git commit -m "stuff"
git commit -m "fixed it"
git commit -m "asdf"
git commit -m "changes"
```

**The Golden Rule**: Write commit messages for your future self (or teammates) who will need to understand what changed and why.

**Commit Message Format** (Professional Style):

```
Short summary (50 chars or less)

More detailed explanation if needed. Wrap at 72 characters.
Explain the problem that this commit solves, or what the
commit accomplishes.

- Bullet points are okay
- Use present tense: "Add feature" not "Added feature"
- Be specific but concise
```

**What Makes a Good Commit**:

✅ **Do**:
- Commit related changes together
- Commit often (small, logical units)
- Write clear messages
- Test before committing

❌ **Don't**:
- Mix unrelated changes
- Commit broken code (if possible)
- Commit sensitive data
- Use vague messages

**Common Mistakes**:

❌ **Committing without staging**:
```bash
# Changed file.txt
git commit -m "Update file"  # ❌ Nothing staged!
# Correct:
git add file.txt
git commit -m "Update file"
```

❌ **Committing too much at once**:
```bash
git add .
git commit -m "Lots of stuff"  # ❌ What stuff?
# Better: Separate commits for different changes
```

❌ **Forgetting to configure user info**:
```bash
# First time committing without config
git commit -m "First commit"
# Error: Please tell me who you are
# Fix:
git config user.name "Your Name"
git config user.email "you@example.com"
```

**When NOT to Use**:
- When you have nothing staged
- Before testing your changes (when possible)
- With incomplete features (unless deliberately saving work)

### git log

**What It Does**: Shows the commit history

**When to Use**: To view past commits, find when something changed, or explore history

**Syntax**:
```bash
git log [options]
```

**Basic Output**:

```bash
$ git log

commit a3f5e2c8d4b6f1e9c7a5b3d1f8e6c4a2b0d9e7f5 (HEAD -> main)
Author: Jane Smith 
Date:   Mon Feb 5 14:23:00 2026 -0800

    Add user authentication

commit 7c8e9a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f
Author: Jane Smith 
Date:   Mon Feb 5 10:15:00 2026 -0800

    Initial commit: Add README
```

**Useful Flags**:

```bash
# One line per commit (much cleaner)
git log --oneline
# Output:
# a3f5e2c (HEAD -> main) Add user authentication
# 7c8e9a1 Initial commit: Add README

# Show last N commits
git log -n 5
git log -5  # Same thing

# Show commits with files changed
git log --stat

# Show commits with actual changes (diff)
git log -p
git log --patch  # Same thing

# Pretty format with graph
git log --oneline --graph --all
# Shows branch structure visually

# See commits by specific author
git log --author="Jane"

# See commits with specific message
git log --grep="bug fix"

# See commits that modified a specific file
git log -- index.html

# See commits in date range
git log --since="2 weeks ago"
git log --after="2026-01-01" --before="2026-02-01"
```

**Most Useful Combinations**:

```bash
# Beautiful commit history
git log --oneline --graph --decorate --all

# Recent activity
git log --oneline -10

# What changed in each commit
git log --oneline --stat

# Full details of last commit
git log -1 -p
```

**Understanding the Output**:

```
commit a3f5e2c8d4b6...  ← SHA-1 hash (unique ID)
(HEAD -> main)          ← Branch pointers
Author: Jane <jane@...> ← Who made the commit
Date: Mon Feb 5...      ← When it was made
                        
    Add user auth...    ← Commit message
```

**Visual Graph** (`--graph`):

```
* a3f5e2c (HEAD -> main) Merge feature
|\
| * 9d8c7b6 (feature) Add feature
| * 3a2b1c0 Work on feature
|/
* 7c8e9a1 Initial commit
```

**When NOT to Use**:
- If you just want to see current status (use `git status` instead)
- If you want to see file contents (use `cat` or your editor)

**Common Mistake**: Overwhelming yourself with too much information
```bash
git log -p  # ❌ Shows every diff, can be huge
# Better for quick overview:
git log --oneline
```

### Complete Beginner Workflow

Let's put it all together with a realistic example:

**Scenario**: You're building a website. You've just finished adding a contact page.

```bash
# 1. Check current status
$ git status
On branch main
nothing to commit, working tree clean

# 2. Create new files
$ echo "Contact Us" > contact.html
$ echo ".email { color: blue; }" > contact.css

# 3. Check status again
$ git status
Untracked files:
  contact.html
  contact.css

# 4. Stage the new files
$ git add contact.html contact.css

# 5. Check status (see they're staged)
$ git status
Changes to be committed:
  new file: contact.html
  new file: contact.css

# 6. Commit with message
$ git commit -m "Add contact page with basic styling"
[main f8d7c2a] Add contact page with basic styling
 2 files changed, 2 insertions(+)
 create mode 100644 contact.html
 create mode 100644 contact.css

# 7. View the history
$ git log --oneline
f8d7c2a (HEAD -> main) Add contact page with basic styling
a3f5e2c Add user authentication
7c8e9a1 Initial commit: Add README

# 8. Oh wait, found a typo in contact.html
$ nano contact.html  # Fix the typo

# 9. Check what changed
$ git status
Changes not staged for commit:
  modified: contact.html

# 10. Stage and commit the fix
$ git add contact.html
$ git commit -m "Fix typo in contact page heading"

# 11. View updated history
$ git log --oneline
e9c6d1b (HEAD -> main) Fix typo in contact page heading
f8d7c2a Add contact page with basic styling
a3f5e2c Add user authentication
7c8e9a1 Initial commit: Add README
```

**The Pattern** (repeat forever):

1. **Make changes** (edit files)
2. **git status** (see what changed)
3. **git add** (stage the changes)
4. **git status** (verify staging)
5. **git commit** (save the snapshot)
6. **git log** (see the history)

**Memory Aid**:

```
Change → Status → Add → Status → Commit → Log
   ↑                                        ↓
   └────────────────────────────────────────┘
               (repeat)
```

---

# Part 2: Building Skills (Intermediate)

## 5. Branches in Depth

### What Branches Really Are

Time for the truth: **Branches are just movable labels pointing to commits**.

That's it. That's the entire concept. Everything else is detail.

```
Before creating a branch:

main → commit1 → commit2 → commit3
                            ↑
                           HEAD
```

```
After creating "feature" branch:

                           main
                            ↓
commit1 → commit2 → commit3
                            ↑
                         feature
                            ↑
                           HEAD
```

**What just happened?** Git created a new label called "feature" pointing to the same commit as "main", and moved HEAD to point to feature.

**After making a commit on feature branch**:

```
                                  feature
                                    ↓
commit1 → commit2 → commit3 → commit4
                      ↑             ↑
                     main          HEAD
```

**Key Insight**: Branches don't contain commits. Branches point to commits. The commits form a chain.

### Creating and Switching Branches

**Creating a Branch**:

```bash
# Create a new branch (but stay on current branch)
git branch feature-login

# Verify it was created
git branch
# Output:
# * main            ← asterisk shows current branch
#   feature-login
```

**Switching Branches**:

```bash
# Old way (still works)
git checkout feature-login

# New way (Git 2.23+, clearer)
git switch feature-login
```

**Create and Switch in One Step**:

```bash
# Old way
git checkout -b feature-login

# New way (recommended)
git switch -c feature-login
```

**What Happens When You Switch**:
1. HEAD moves to point to the new branch
2. Files in working directory change to match that branch
3. Git is fast - switching is nearly instant

**Visual Example**:

```bash
# On main branch
$ git branch
* main

$ ls
index.html  style.css

# Create and switch to feature branch
$ git switch -c add-footer

$ git branch
  main
* add-footer

# Create a new file
$ echo "Footer content" > footer.html

$ git add footer.html
$ git commit -m "Add footer"

# Switch back to main
$ git switch main

$ ls
index.html  style.css  # footer.html is gone!

# Switch back to feature
$ git switch add-footer

$ ls
index.html  style.css  footer.html  # It's back!
```

**Important Rules**:

✅ **Before Switching Branches**:
- Commit your changes, OR
- Stash your changes (covered later), OR
- Be okay with losing them

❌ **Don't switch with uncommitted changes** (unless intentional):
```bash
$ git status
Changes not staged:
  modified: index.html

$ git switch other-branch
# Git might refuse if there would be conflicts
```

### git checkout vs git switch

**The History**: `git checkout` does too many things. Git 2.23 (2019) introduced `git switch` and `git restore` to split the responsibilities.

**git checkout** (old, still works):
- Switch branches
- Create branches
- Restore files
- Create detached HEAD
- ...and more

**git switch** (new, recommended):
- Switch branches
- Create branches
- That's it

**git restore** (new, recommended):
- Restore files
- Unstage files
- That's it

**Translation Table**:

| Old Command | New Command | What It Does |
|-------------|-------------|--------------|
| `git checkout branch` | `git switch branch` | Switch to branch |
| `git checkout -b new` | `git switch -c new` | Create and switch |
| `git checkout -- file` | `git restore file` | Discard changes to file |
| `git checkout HEAD~2` | `git switch --detach HEAD~2` | Detached HEAD |

**Recommendation**: Use `git switch` and `git restore` for clarity. But understand `git checkout` because you'll see it everywhere in older tutorials.

### Branching from Branches

You can create a branch from any branch, not just `main`.

```bash
# On main branch
$ git switch -c feature-A

# Make some commits
$ git commit -m "Work on feature A"

# Create a sub-feature branch
$ git switch -c feature-A-experiment

# Make some commits
$ git commit -m "Try experimental approach"
```

**Visual**:

```
                         feature-A-experiment
                                ↓
main → c1 → c2 → c3 → c4 → c5
                 ↑
            feature-A
```

**Use Cases**:
- Experiment without affecting your main feature branch
- Multiple developers working on sub-features
- Trying risky changes

**Merging Back**:
```bash
# Test succeeded, merge experiment into feature-A
$ git switch feature-A
$ git merge feature-A-experiment

# Then later, merge feature-A into main
$ git switch main
$ git merge feature-A
```

### Branch Naming Conventions

**Common Patterns**:

```bash
# Feature branches
feature/user-authentication
feature/payment-integration
feat/dark-mode

# Bug fixes
fix/login-crash
bugfix/broken-link
hotfix/security-vulnerability

# Experiments
experiment/new-algorithm
test/performance-optimization
spike/research-new-library

# Releases
release/v1.2.0
release/2026-02-01
```

**Rules of Thumb**:
- Use lowercase
- Use hyphens (not underscores or spaces)
- Be descriptive
- Include ticket numbers if you use an issue tracker
  - `feature/JIRA-123-add-export`

**Personal Workflow** (solo developer):
```bash
main                    # Stable code
dev                     # Development
feature/NAME            # New features
fix/NAME                # Bug fixes
```

**Team Workflow** (common):
```bash
main                    # Production
develop                 # Next release
feature/NAME            # New features
release/VERSION         # Release prep
hotfix/NAME             # Urgent fixes
```

### Deleting Branches

**Delete a Merged Branch**:

```bash
# Safe delete (only if fully merged)
git branch -d feature-login

# If not merged, Git refuses:
# error: The branch 'feature-login' is not fully merged.

# Force delete (even if not merged)
git branch -D feature-login  # ⚠️ Be careful!
```

**Delete a Remote Branch**:

```bash
git push origin --delete feature-login
```

**When to Delete Branches**:
- ✅ After merging into main
- ✅ After deciding not to use the feature
- ✅ After experiment fails

**When NOT to Delete**:
- ❌ While still working on it
- ❌ If not merged and you might want it later
- ❌ `main` or other important branches

**See All Branches**:

```bash
# Local branches
git branch

# Remote branches
git branch -r

# All branches (local and remote)
git branch -a

# See last commit on each branch
git branch -v
```

---

## 6. Viewing History and Changes

### git log (All the Useful Flags)

We covered basic `git log` earlier. Now let's explore power-user features.

**Most Useful Everyday Aliases**:

```bash
# Beautiful commit tree
git log --oneline --graph --all --decorate

# Recent changes
git log --oneline -10

# See what changed
git log --stat

# Full diff of recent commits
git log -p -2
```

**Filtering by Author**:

```bash
# See all your commits
git log --author="Jane"

# See someone else's commits
git log --author="john@example.com"
```

**Filtering by Date**:

```bash
# Last 2 weeks
git log --since="2 weeks ago"

# Specific date range
git log --after="2026-01-01" --before="2026-02-01"

# Yesterday
git log --since="yesterday"

# Last 3 days
git log --since="3 days ago"
```

**Filtering by Message**:

```bash
# Find commits mentioning "bug"
git log --grep="bug"

# Case insensitive
git log --grep="BUG" -i

# Multiple search terms (OR)
git log --grep="bug" --grep="fix"

# Multiple terms (AND)
git log --grep="bug" --grep="fix" --all-match
```

**Filtering by File**:

```bash
# See commits that changed index.html
git log -- index.html

# See commits that changed any CSS file
git log -- *.css

# See commits in specific directory
git log -- src/components/
```

**Filtering by Content** (Advanced):

```bash
# Find commits that added or removed "function login"
git log -S "function login"

# Find commits that changed lines matching regex
git log -G "function.*login"
```

**Pretty Formatting**:

```bash
# Custom format
git log --pretty=format:"%h - %an, %ar : %s"
# Output: a3f5e2c - Jane Smith, 2 hours ago : Add login feature

# Format codes:
# %h  = short hash
# %H  = full hash
# %an = author name
# %ae = author email
# %ar = author date, relative
# %ad = author date
# %s  = subject (commit message)
# %b  = body
```

**Combining Filters**:

```bash
# Jane's commits from last week mentioning "login"
git log --author="Jane" --since="1 week ago" --grep="login"

# Recent commits to index.html with diffs
git log -p -5 -- index.html

# Visual history of feature branches
git log --oneline --graph --all --since="1 month ago"
```

**Practical Examples**:

```bash
# "What did I do yesterday?"
git log --author="$(git config user.name)" --since="yesterday" --oneline

# "When was this file last modified?"
git log -1 --format="%ar" -- path/to/file

# "Show me the last 5 commits with changes"
git log -5 --stat

# "Find the commit that broke the login"
git log --all --oneline -- src/login.js
```

**Performance Tip**: For huge repositories, limit the scope:
```bash
# Only commits reachable from current branch
git log

# All commits (slow on big repos)
git log --all
```

### git diff (All Variants)

**What It Does**: Shows differences between various states

**Basic Diff** (unstaged changes):

```bash
# Show what you changed but haven't staged
git diff

# Output:
diff --git a/index.html b/index.html
index a3f5e2c..7c8e9a1 100644
--- a/index.html
+++ b/index.html
@@ -1,3 +1,4 @@
 
 
-  Hello
+  Hello World
+  Welcome!
 
```

**Reading Diff Output**:
- `---` = old version
- `+++` = new version
- Lines starting with `-` were removed
- Lines starting with `+` were added
- Lines without `-` or `+` are context

**Diff Staged Changes**:

```bash
# Show what you staged (will be in next commit)
git diff --staged
# or
git diff --cached  # Same thing
```

**Diff Specific File**:

```bash
# Unstaged changes in one file
git diff index.html

# Staged changes in one file
git diff --staged index.html
```

**Diff Between Commits**:

```bash
# Diff between two commits
git diff a3f5e2c 7c8e9a1

# Diff between commit and current state
git diff a3f5e2c

# Diff between commit and HEAD
git diff a3f5e2c HEAD
```

**Diff Between Branches**:

```bash
# See what's different in feature branch vs main
git diff main feature

# What changes would be merged
git diff main...feature  # Three dots!
```

**Word Diff** (better for prose):

```bash
# Instead of line-by-line, show word-by-word
git diff --word-diff

# Good for documentation or text files
```

**Statistics**:

```bash
# Just show which files changed
git diff --stat

# Output:
# index.html | 5 +++--
# style.css  | 2 +-
# 2 files changed, 5 insertions(+), 3 deletions(-)
```

**Ignore Whitespace**:

```bash
# Ignore whitespace changes (useful for reformatted code)
git diff -w
git diff --ignore-all-space
```

**Diff Tools** (visual):

```bash
# Use configured diff tool (like meld, kdiff3, etc.)
git difftool

# Use specific tool
git difftool --tool=meld
```

**Practical Examples**:

```bash
# "What did I change since last commit?"
git diff

# "What am I about to commit?"
git diff --staged

# "What changed in the last commit?"
git diff HEAD~1 HEAD

# "What's different between my branch and main?"
git diff main..feature

# "Show me changes to JavaScript files only"
git diff -- "*.js"
```

**Common Workflows**:

```bash
# Before committing
$ git diff                 # Review unstaged changes
$ git add .                # Stage changes
$ git diff --staged        # Review staged changes
$ git commit -m "message"  # Commit

# Before merging
$ git diff main..feature   # See what would be merged
$ git merge feature        # Merge
```

### Comparing Branches

**See Commits in One Branch But Not Another**:

```bash
# Commits in feature but not in main
git log main..feature

# Commits in main but not in feature
git log feature..main

# Visual comparison
git log --oneline --graph main..feature
```

**Three-Dot vs Two-Dot**:

```bash
# Two dots: commits reachable from B but not from A
git log A..B

# Three dots: commits in either A or B, but not both
git log A...B

# For diff, three dots means "compare merge base"
git diff main...feature
# Shows changes in feature since it branched from main
```

**See All Diverging Commits**:

```bash
git log --left-right --oneline main...feature

# Output:
# < a3f5e2c Commit in main
# > 7c8e9a1 Commit in feature
# > 9d8c7b6 Another commit in feature
```

### Finding Specific Changes

**Find When a Function Was Introduced**:

```bash
git log -S "function login" --source --all
```

**Find When a Line Changed**:

```bash
# Show line-by-line history of a file
git blame index.html

# Output shows: commit, author, timestamp for each line
```

**Find Deleted File**:

```bash
# Find commits that deleted files
git log --diff-filter=D --summary

# Find when specific file was deleted
git log --all --full-history -- path/to/file
```

**Find Commit That Introduced a Bug** (binary search):

```bash
git bisect start
git bisect bad           # Current commit is bad
git bisect good a3f5e2c  # Known good commit
# Git checks out middle commit
# Test it, then mark:
git bisect good          # If it works
git bisect bad           # If it's broken
# Repeat until Git finds the bad commit
git bisect reset         # When done
```

---

## 7. Ignoring Files

### What .gitignore Does

**Purpose**: Tell Git to ignore certain files (don't track them)

**Common Use Cases**:
- Build outputs (`dist/`, `build/`)
- Dependencies (`node_modules/`, `venv/`)
- IDE files (`.vscode/`, `.idea/`)
- OS files (`.DS_Store`, `Thumbs.db`)
- Secrets (`.env`, `secrets.json`)
- Log files (`*.log`)

**How It Works**: Create a file named `.gitignore` in your repository root:

```bash
# Create .gitignore
touch .gitignore

# Edit it
nano .gitignore
```

### Pattern Rules Explained

**Basic Patterns**:

```gitignore
# Ignore specific file
secrets.txt

# Ignore all files with extension
*.log

# Ignore directory
node_modules/

# Ignore files in specific directory
build/*.js

# Ignore all .pdf files in any directory
**/*.pdf
```

**Pattern Symbols**:

```gitignore
# * = wildcard (anything)
*.txt           # All .txt files

# ** = recursive wildcard
**/logs         # logs directory anywhere
logs/**         # All files in logs directory
**/*.log        # All .log files anywhere

# ? = single character
file?.txt       # file1.txt, fileA.txt (not file10.txt)

# ! = negation (exception)
*.log           # Ignore all .log files
!important.log  # Except this one

# / at end = directory only
build/          # Ignore build directory

# / at start = root directory only
/TODO.txt       # Only in root, not in subdirectories

# # = comment
# This is a comment
```

**Advanced Examples**:

```gitignore
# Ignore all .txt files except README.txt
*.txt
!README.txt

# Ignore all files in temp/ except temp/keep.txt
temp/*
!temp/keep.txt

# Ignore .env files but not .env.example
.env
!.env.example
```

### Common .gitignore Templates

**Node.js Project**:

```gitignore
# Dependencies
node_modules/
npm-debug.log
package-lock.json  # Sometimes

# Environment
.env
.env.local

# Build
dist/
build/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

**Python Project**:

```gitignore
# Virtual environment
venv/
env/
ENV/
.venv

# Python cache
__pycache__/
*.pyc
*.pyo
*.pyd

# Distribution
dist/
build/
*.egg-info/

# Environment
.env

# IDE
.vscode/
.idea/
*.swp
*.swo
```

**General Web Project**:

```gitignore
# Build outputs
dist/
build/
public/build/

# Dependencies
node_modules/
vendor/

# Environment variables
.env
.env.local
.env.*.local

# Logs
logs/
*.log

# IDE
.vscode/
.idea/
*.sublime-workspace

# OS
.DS_Store
Thumbs.db
desktop.ini

# Temporary files
*.tmp
*.temp
*.swp
*.swo
*~
```

**Get Templates**: https://github.com/github/gitignore

### When .gitignore Doesn't Work

**Problem**: "I added a file to .gitignore but Git still tracks it!"

**Reason**: .gitignore only affects untracked files. If Git already tracks a file, .gitignore has no effect.

**Solution**: Untrack the file:

```bash
# Remove from Git but keep the file
git rm --cached filename

# Remove directory from Git but keep it
git rm -r --cached node_modules/

# Then commit
git commit -m "Stop tracking node_modules"

# Now .gitignore will work
```

**Complete Example**:

```bash
# Oops, committed secrets.txt
$ git add secrets.txt
$ git commit -m "Add config"

# Add to .gitignore
$ echo "secrets.txt" >> .gitignore

# But Git still shows changes to secrets.txt!
$ git status
  modified: secrets.txt  # Still tracked!

# Untrack it
$ git rm --cached secrets.txt

$ git commit -m "Stop tracking secrets.txt"

# Now changes to secrets.txt are ignored
$ git status
  nothing to commit, working tree clean
```

**Global .gitignore** (for personal preferences):

```bash
# Create global gitignore
git config --global core.excludesfile ~/.gitignore_global

# Add personal preferences
echo ".DS_Store" >> ~/.gitignore_global
echo ".vscode/" >> ~/.gitignore_global
```

**Check If File Is Ignored**:

```bash
git check-ignore -v filename

# Output shows which rule matched (or nothing if not ignored)
```

---

## 8. Stashing: Temporary Storage

### What Stash Is

**The Problem**: You're working on something, but need to switch branches urgently (like to fix a bug), but your current changes aren't ready to commit.

**The Solution**: Stash your changes temporarily.

**Mental Model**: Stash is like a clipboard. You copy your changes, clear your workspace, do other work, then paste them back.

### When to Use It

✅ **Use stash when**:
- Switching branches with uncommitted changes
- Need to pull but have local changes
- Want to try something without committing
- Interrupted by urgent work

❌ **Don't use stash when**:
- Changes are ready to commit (just commit them)
- You want to permanently save work (use a branch)
- You want to share work with others (commit and push)

### Stash Commands

**Basic Stash**:

```bash
# Save current changes and clean working directory
git stash

# Or with a message (recommended)
git stash push -m "WIP: login form"
```

**What Gets Stashed**:
- ✅ Modified tracked files
- ✅ Staged changes
- ❌ Untracked files (by default)
- ❌ Ignored files

**Stash Including Untracked Files**:

```bash
git stash -u
# or
git stash --include-untracked
```

**View Stash List**:

```bash
git stash list

# Output:
# stash@{0}: WIP on main: a3f5e2c Add login form
# stash@{1}: On feature: 7c8e9a1 Experiments
# stash@{2}: WIP on main: 9d8c7b6 Old work
```

**Apply Stashed Changes**:

```bash
# Apply most recent stash (keeps stash)
git stash apply

# Apply specific stash
git stash apply stash@{1}

# Apply and remove from stash list
git stash pop

# Apply specific stash and remove it
git stash pop stash@{1}
```

**Delete Stashed Changes**:

```bash
# Delete most recent stash
git stash drop

# Delete specific stash
git stash drop stash@{1}

# Delete all stashes
git stash clear  # ⚠️ Careful!
```

**View Stash Contents**:

```bash
# Show what's in latest stash
git stash show

# Show full diff
git stash show -p

# Show specific stash
git stash show -p stash@{1}
```

**Create Branch from Stash**:

```bash
# Create a new branch with stashed changes
git stash branch new-branch-name stash@{0}

# Useful when stash has conflicts with current branch
```

### Common Stash Workflows

**Workflow 1: Quick Branch Switch**

```bash
# Working on feature branch
$ git status
Changes not staged:
  modified: feature.js

# Urgent: need to fix bug on main
$ git stash push -m "WIP: halfway through feature X"

$ git switch main
$ # Fix the bug...
$ git add .
$ git commit -m "Fix urgent bug"

# Back to feature branch
$ git switch feature
$ git stash pop
# Continue working
```

**Workflow 2: Try Something Risky**

```bash
# Save current work
$ git stash push -m "Before trying risky refactor"

# Try the risky change
$ # ...make changes...

# Didn't work, restore original
$ git stash pop

# Or: It worked! Commit it
$ git add .
$ git commit -m "Successful refactor"
$ git stash drop  # Don't need the stash anymore
```

**Workflow 3: Stash Specific Files**

```bash
# Stash only specific files
git stash push -m "Just the CSS changes" style.css theme.css

# Everything else remains unstaged
```

**Workflow 4: Multiple Stashes**

```bash
# You can have multiple stashes
$ git stash push -m "Experiment A"
$ # ...work on something else...
$ git stash push -m "Experiment B"

$ git stash list
stash@{0}: Experiment B
stash@{1}: Experiment A

# Apply the older one
$ git stash apply stash@{1}
```

**Common Mistakes**:

❌ **Forgetting what's in a stash**:
```bash
# Always use messages
git stash push -m "What I was doing"
# Not just:
git stash  # ❌ Future you won't remember
```

❌ **Stashing too many things**:
```bash
# 20 stashes later...
git stash list  # ❌ Overwhelming

# Better: Clean up regularly
git stash clear  # Or drop individual stashes
```

❌ **Stashing instead of committing**:
```bash
# If work is done, commit it!
git commit -m "Complete feature"
# Not:
git stash  # ❌ Temporary solution used permanently
```

---

## 9. Merging: Bringing Branches Together

### Fast-Forward Merge

**Scenario**: You created a branch, made commits, but main hasn't changed.

```
Before merge:

main → c1 → c2
              ↘
                c3 → c4 (feature)
```

**Fast-Forward Merge**:

```bash
$ git switch main
$ git merge feature

# Git just moves the 'main' label forward
```

```
After merge:

main → c1 → c2 → c3 → c4
                        ↑
                    (feature)
```

**Characteristics**:
- No new commit created
- Linear history
- Fast and simple
- Git just moves the pointer

**Force Non-Fast-Forward** (create merge commit anyway):

```bash
git merge --no-ff feature

# Creates:
main → c1 → c2 → c3 → c4 → c5 (merge commit)
                 ↘           ↗
                   (feature)
```

**Why?** Preserves the fact that work was done in a branch.

### Three-Way Merge

**Scenario**: Both branches have new commits.

```
Before merge:

              c3 → c4 (feature)
             ↗
main → c1 → c2
              ↘
                c5 → c6 (main)
```

**Three-Way Merge**:

```bash
$ git switch main
$ git merge feature

# Git creates a new "merge commit"
```

```
After merge:

              c3 → c4 ──────┐
             ↗              ↓
main → c1 → c2 → c5 → c6 → c7 (merge commit)
```

**Characteristics**:
- Creates a new commit with two parents
- Preserves both branches' history
- Shows where branches diverged and merged

**The Merge Commit**:

```bash
git log --oneline --graph

# Output:
# *   c7 Merge branch 'feature' into main
# |\
# | * c4 Feature work
# | * c3 Start feature
# * | c6 Work on main
# * | c5 More work on main
# |/
# * c2 Common ancestor
```

### Merge Conflicts: Why They Happen

**Conflict** = Same part of same file changed in both branches.

**Example**:

**main branch** (index.html):
```html
Welcome to My Site
```

**feature branch** (index.html):
```html
Welcome to Our Amazing Platform
```

Both changed the same line! Git doesn't know which to keep.

**When Conflicts Happen**:
- ✅ Same line edited in both branches
- ✅ One branch edits, other deletes
- ✅ Both branches add different content in same place
- ❌ Changes in different files (no conflict)
- ❌ Changes in different parts of same file (usually no conflict)

### How to Resolve Conflicts

**The Process**:

```bash
$ git merge feature

# Output:
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.

$ git status
Both modified:   index.html
```

**Open the Conflicted File**:

```html


<<<<<<< HEAD
Welcome to My Site
=======
Welcome to Our Amazing Platform
>>>>>>> feature


```

**Conflict Markers Explained**:

```
<<<<<<< HEAD
Your current branch's version
=======
The branch you're merging in
>>>>>>> feature
```

**Resolution Steps**:

1. **Decide which to keep** (or combine):

```html

Welcome to My Site


Welcome to Our Amazing Platform


Welcome to Our Amazing Site


Welcome
```

2. **Remove the conflict markers**:

```html


Welcome to Our Amazing Site


```

3. **Stage the resolved file**:

```bash
git add index.html
```

4. **Complete the merge**:

```bash
git commit
# Git opens editor with default message
# "Merge branch 'feature' into main"
# Save and close
```

**Multiple Conflicts**:

```bash
$ git status
Both modified:   index.html
Both modified:   style.css
Both modified:   script.js

# Resolve each file
$ nano index.html  # Resolve
$ git add index.html

$ nano style.css   # Resolve
$ git add style.css

$ nano script.js   # Resolve
$ git add script.js

# Commit when all resolved
$ git commit
```

**Abort Merge** (if you mess up):

```bash
# Cancel the merge, go back to before
git merge --abort
```

**Merge Tools**:

```bash
# Use visual merge tool
git mergetool

# Tools like meld, kdiff3, etc.
# Shows 3 versions side-by-side
```

### Merge Best Practices

**Before Merging**:

```bash
# 1. Make sure working directory is clean
git status  # Should show nothing

# 2. Update both branches
git switch main
git pull origin main

git switch feature
git pull origin feature

# 3. Merge main into feature first (optional but recommended)
git merge main
# Resolve conflicts here, in feature branch

# 4. Now merge feature into main
git switch main
git merge feature  # Should be clean!
```

**Why Merge main into feature first?**
- Conflicts are resolved in feature branch
- main branch stays clean
- Easier to test before merging to main

**Good Commit Messages**:

```bash
# ✅ GOOD
git commit -m "Merge feature/user-auth into main

Resolved conflicts in:
- auth.js: Kept feature version (new auth flow)
- config.js: Combined both approaches"

# ❌ BAD
git commit -m "merge stuff"
```

**Delete Merged Branches**:

```bash
# After successful merge
git branch -d feature

# Git refuses if not merged
# Force delete if you're sure
git branch -D feature
```

---

## 10. Working with Remote Repositories

### Understanding Remotes

**Remote** = A version of your repository hosted somewhere else (usually a server).

**Common Remotes**:
- GitHub, GitLab, Bitbucket
- Your own server
- Another directory on your computer (for practice)

**Mental Model**: Your repository and the remote repository are separate. You explicitly sync between them.

```
┌──────────────────────┐         ┌──────────────────────┐
│  Your Computer       │         │  Remote (GitHub)     │
│                      │         │                      │
│  Local Repository    │  sync   │  Remote Repository   │
│  - Your commits      │  ←───→  │  - Team's commits    │
│  - Your branches     │         │  - Shared branches   │
└──────────────────────┘         └──────────────────────┘
```

### git remote

**View Remotes**:

```bash
# List remotes
git remote

# Output:
# origin

# Verbose (show URLs)
git remote -v

# Output:
# origin  https://github.com/user/repo.git (fetch)
# origin  https://github.com/user/repo.git (push)
```

**Add a Remote**:

```bash
# Add remote named 'origin'
git remote add origin https://github.com/user/repo.git

# Add another remote
git remote add upstream https://github.com/original/repo.git
```

**Remove a Remote**:

```bash
git remote remove origin
```

**Rename a Remote**:

```bash
git remote rename origin github
```

**Change Remote URL**:

```bash
git remote set-url origin https://new-url.git
```

**Typical Setup** (after cloning):

```bash
$ git remote -v
origin  https://github.com/yourname/repo.git (fetch)
origin  https://github.com/yourname/repo.git (push)

# If it's a fork, add upstream
$ git remote add upstream https://github.com/original/repo.git

$ git remote -v
origin    https://github.com/yourname/repo.git (fetch)
origin    https://github.com/yourname/repo.git (push)
upstream  https://github.com/original/repo.git (fetch)
upstream  https://github.com/original/repo.git (push)
```

### git fetch vs git pull

**git fetch**: Download changes but don't merge

**git pull**: Download changes AND merge

```
git pull = git fetch + git merge
```

**git fetch**:

```bash
# Fetch from origin
git fetch origin

# Fetch all remotes
git fetch --all
```

**What happens**:
- Downloads new commits from remote
- Updates remote branch pointers (origin/main)
- Does NOT change your working directory
- Does NOT change your local branches

```
Before fetch:

Local:         main → c1 → c2
                             ↑
                            HEAD

Remote:        origin/main → c1 → c2 → c3 → c4
```

```
After fetch:

Local:         main → c1 → c2
                       ↑
                      HEAD

               origin/main → c1 → c2 → c3 → c4
```

You can now inspect the changes before merging:

```bash
# See what's new
git log main..origin/main

# View the changes
git diff main origin/main

# When ready, merge
git merge origin/main
```

**git pull**:

```bash
# Fetch and merge in one step
git pull origin main
```

**Equivalent to**:

```bash
git fetch origin
git merge origin/main
```

**Pull with Rebase** (advanced, cleaner history):

```bash
git pull --rebase origin main
```

**When to Use Each**:

| Use fetch when | Use pull when |
|----------------|---------------|
| Want to review changes first | Trust the changes |
| Working carefully | Quick sync |
| Multiple remotes | Daily workflow |
| Checking before merge | Convenient |

**Recommended Workflow**:

```bash
# Cautious approach
git fetch origin
git log main..origin/main  # Review changes
git diff main origin/main  # See diffs
git merge origin/main      # Merge when ready

# Quick approach (most common)
git pull origin main
```

### git push

**What It Does**: Upload your local commits to the remote

**Basic Syntax**:

```bash
git push  

# Examples:
git push origin main
git push origin feature-login
```

**First Push** (new branch):

```bash
# Create and push new branch
git push -u origin feature-login

# -u sets up tracking (only needed once)
# After this, you can just use:
git push
```

**What `-u` Does** (set upstream):

```bash
# Long form
git push origin feature-login

# After setting upstream with -u
git push  # Knows where to push
git pull  # Knows where to pull from
```

**Push All Branches**:

```bash
git push --all origin
```

**Push Tags**:

```bash
git push --tags origin
```

**Force Push** (⚠️ DANGEROUS):

```bash
git push --force origin main

# Safer version (refuses if remote has new commits)
git push --force-with-lease origin main
```

**When to Force Push**:
- ✅ On your personal feature branch
- ✅ After rewriting history (and you're sure)
- ❌ On main/shared branches
- ❌ If others are using the branch

**Delete Remote Branch**:

```bash
git push origin --delete feature-login
```

**Common Errors**:

**Error**: "Updates were rejected because the remote contains work..."

**Meaning**: Someone else pushed commits. You need to pull first.

**Fix**:

```bash
git pull origin main
# Resolve any conflicts
git push origin main
```

**Error**: "src refspec main does not match any"

**Meaning**: The branch doesn't exist locally.

**Fix**:

```bash
# Make sure you're on the right branch
git branch

# Or create the branch
git switch -c main
```

### Pull Requests Explained

**What Is It**: A request to merge your branch into another branch.

**Why "Pull" Request?** Historical name. You're asking the maintainer to "pull" your changes.

**Modern Name**: Some platforms call it "Merge Request" (GitLab).

**The Workflow**:

```bash
# 1. Fork the repository on GitHub
# (Click "Fork" button)

# 2. Clone your fork
git clone https://github.com/yourusername/repo.git

# 3. Create a feature branch
git switch -c feature/add-dark-mode

# 4. Make changes
# ...edit files...

# 5. Commit
git add .
git commit -m "Add dark mode toggle"

# 6. Push to your fork
git push origin feature/add-dark-mode

# 7. Create Pull Request on GitHub
# (Click "New Pull Request" button)

# 8. Wait for review and feedback

# 9. Make requested changes
# ...edit files...
git add .
git commit -m "Address review comments"
git push origin feature/add-dark-mode

# 10. PR gets merged!
```

**PR Best Practices**:

✅ **Do**:
- Keep PRs focused and small
- Write clear description
- Reference issue numbers
- Respond to feedback
- Keep branch updated with main

❌ **Don't**:
- Mix unrelated changes
- Make huge PRs (1000+ lines)
- Force push after people review
- Ignore feedback

**Updating Your PR**:

```bash
# Main has new commits, update your branch
git switch main
git pull origin main

git switch feature/add-dark-mode
git merge main
# Or rebase (covered later)
git rebase main

git push origin feature/add-dark-mode
```

---

## 11. Safe Workflows

### Solo Developer Workflow

**Simple and Effective**:

```
main branch ──────────────────────────────────
                ↓                      ↑
           feature branch ──────────────
```

**Process**:

```bash
# 1. Start with clean main
git switch main
git pull origin main

# 2. Create feature branch
git switch -c feature/new-thing

# 3. Work and commit regularly
git add .
git commit -m "Progress on new thing"
# ...continue working...
git commit -m "More progress"

# 4. Feature is done, update main
git switch main
git pull origin main  # Get any changes

# 5. Merge feature
git merge feature/new-thing

# 6. Push to remote
git push origin main

# 7. Delete feature branch
git branch -d feature/new-thing
```

**When to Branch** (solo):
- ✅ Trying something experimental
- ✅ Big feature that takes days
- ✅ Want to switch between tasks
- ❌ Tiny changes (just commit to main)

### Team Workflow

**Feature Branch Workflow**:

```
main ────────────────────────────────────────
  ↓                                    ↑
  ├── alice/feature-A ──────────────────┤
  ├── bob/feature-B ────────────────────┤
  └── charlie/bugfix-X ─────────────────┘
```

**Process**:

```bash
# Alice's workflow
$ git switch -c alice/login-form
$ # Work...
$ git push -u origin alice/login-form
# Create PR on GitHub

# Bob's workflow (same time)
$ git switch -c bob/dark-mode
$ # Work...
$ git push -u origin bob/dark-mode
# Create PR on GitHub

# PRs get reviewed and merged
# Everyone updates their main
$ git switch main
$ git pull origin main
```

**Rules**:
1. Never commit directly to main
2. Always use branches
3. Always use Pull Requests
4. Get code reviews
5. Keep main deployable

**Branch Naming** (team):

```bash
# Include your name or initials
alice/feature-login
bob/fix-crash

# Or use issue numbers
feature/GH-123-add-auth
bugfix/GH-456-fix-crash

# Or category prefixes
feature/user-authentication
bugfix/login-crash
hotfix/security-patch
```

### Feature Branch Workflow

**The Cycle**:

```
1. Update main
2. Create feature branch
3. Work on feature
4. Keep branch updated
5. Create PR
6. Get reviewed
7. Merge
8. Delete branch
9. Repeat
```

**Detailed Steps**:

```bash
# 1. Update main
git switch main
git pull origin main

# 2. Create feature branch
git switch -c feature/add-comments

# 3. Work and commit
git add comments.js
git commit -m "Add comment component"

git add comments.css
git commit -m "Style comments"

# 4. Push early and often
git push -u origin feature/add-comments

# 5. Keep updated (if main changes)
git fetch origin
git merge origin/main
# Or rebase (covered later)

# 6. Create PR (on GitHub/GitLab)
# Add description, link issues

# 7. Address review feedback
git add comments.js
git commit -m "Fix indentation per review"
git push origin feature/add-comments

# 8. PR gets approved and merged

# 9. Clean up
git switch main
git pull origin main
git branch -d feature/add-comments
git push origin --delete feature/add-comments
```

**Keeping Branch Updated**:

```bash
# Option 1: Merge (preserves history)
git switch feature/add-comments
git merge main

# Option 2: Rebase (cleaner history)
git switch feature/add-comments
git rebase main

# Push after merge
git push origin feature/add-comments

# Push after rebase (need force push)
git push --force-with-lease origin feature/add-comments
```

**Dealing with Conflicts**:

```bash
# Update your branch from main
git merge main
# Conflict!

# Fix conflicts
nano conflicted-file.js
git add conflicted-file.js
git commit

# Push
git push origin feature/add-comments
```

**Emergency Hotfix Workflow**:

```bash
# Critical bug in production!

# 1. Branch from main
git switch main
git pull origin main
git switch -c hotfix/critical-bug

# 2. Fix the bug
git add fix.js
git commit -m "Fix critical security bug"

# 3. Push and create urgent PR
git push -u origin hotfix/critical-bug
# Create PR, mark as urgent

# 4. Fast-track review and merge

# 5. Everyone updates
git switch main
git pull origin main
```

---

# Part 3: Advanced Techniques

## 12. Rewriting History

### git reset (soft, mixed, hard)

**⚠️ WARNING**: These commands change history. Use with caution.

**What It Does**: Moves the current branch pointer (and optionally changes staging/working directory)

**The Three Modes**:

```
git reset --soft   → Move HEAD, keep staging and working directory
git reset --mixed  → Move HEAD, update staging, keep working directory (DEFAULT)
git reset --hard   → Move HEAD, update staging AND working directory
```

**Visual Explanation**:

```
Current state:

main → c1 → c2 → c3 → c4
                        ↑
                      HEAD
```

**After `git reset --soft HEAD~2`**:

```
main → c1 → c2 → c3 → c4
             ↑
           HEAD

Staging area: Contains changes from c3 and c4
Working directory: Contains changes from c3 and c4
```

**After `git reset --mixed HEAD~2`** (default):

```
main → c1 → c2 → c3 → c4
             ↑
           HEAD

Staging area: Empty
Working directory: Contains changes from c3 and c4
```

**After `git reset --hard HEAD~2`**:

```
main → c1 → c2 → c3 → c4 (commits still exist, just not reachable)
             ↑
           HEAD

Staging area: Empty
Working directory: Matches c2 (changes from c3 and c4 are GONE)
```

**Common Uses**:

**Undo Last Commit (Keep Changes)**:

```bash
# Undo commit, keep changes staged
git reset --soft HEAD~1

# Undo commit, keep changes unstaged
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

**Completely Discard Last Commit**:

```bash
git reset --hard HEAD~1
# ⚠️ Changes are GONE
```

**Unstage Files**:

```bash
# Unstage everything
git reset

# Unstage specific file
git reset file.txt
```

**Move to Specific Commit**:

```bash
# Reset to specific commit
git reset --hard a3f5e2c

# ⚠️ All commits after a3f5e2c become unreachable
```

**When to Use Each**:

| Mode | Use When |
|------|----------|
| `--soft` | Want to recommit changes differently |
| `--mixed` | Want to unstage but keep changes |
| `--hard` | Want to discard everything (⚠️ DANGEROUS) |

**The GOLDEN RULE**: 

**NEVER use `git reset` on commits that have been pushed to a shared repository.**

If you do, you'll cause problems for everyone else. Use `git revert` instead (next section).

### git revert

**What It Does**: Creates a NEW commit that undoes a previous commit

**Key Difference from reset**:
- ✅ `git revert`: Adds to history (safe for shared repos)
- ⚠️ `git reset`: Rewrites history (dangerous for shared repos)

**Syntax**:

```bash
git revert 
```

**Visual Example**:

```
Before:

main → c1 → c2 → c3 → c4
                        ↑
                      HEAD
```

```
After `git revert c3`:

main → c1 → c2 → c3 → c4 → c5 (revert of c3)
                              ↑
                            HEAD
```

**c5 undoes changes from c3, but c3 still exists in history.**

**Examples**:

```bash
# Revert the last commit
git revert HEAD

# Git opens editor for commit message
# Default: "Revert 'original message'"

# Revert specific commit
git revert a3f5e2c

# Revert without opening editor
git revert --no-edit HEAD

# Revert multiple commits
git revert c3..c1  # Revert c3, c2, c1 (in that order)
```

**When Reverting Creates Conflicts**:

```bash
$ git revert a3f5e2c
# CONFLICT: ...

# Resolve conflicts
$ nano conflicted-file.js
$ git add conflicted-file.js

# Continue revert
$ git revert --continue

# Or abort
$ git revert --abort
```

### When to Use Which

**Decision Table**:

| Situation | Use This | Why |
|-----------|----------|-----|
| Undo last local commit | `git reset --soft HEAD~1` | Keep changes, recommit |
| Completely discard last commit | `git reset --hard HEAD~1` | ⚠️ ONLY if not pushed |
| Undo commit already pushed | `git revert HEAD` | Safe, adds to history |
| Unstage files | `git reset file.txt` | Don't need --mixed |
| Go back 5 commits locally | `git reset --hard HEAD~5` | ⚠️ ONLY if not pushed |
| Undo bad merge | `git revert -m 1 <merge-commit>` | Safe for pushed merges |
| "Oops, wrong commit message" | `git commit --amend` | ONLY if not pushed |

**The Decision Flow**:

```
Have you pushed the commit?
    │
    ├─ NO → Safe to use git reset
    │       - Soft: Keep changes
    │       - Mixed: Unstage changes
    │       - Hard: Discard everything
    │
    └─ YES → Use git revert
            - Creates new commit
            - Safe for shared repos
            - Preserves history
```

**Examples**:

**Scenario 1**: Wrong commit message, not pushed

```bash
git commit -m "fix bug"  # Oops, too vague

# Fix it
git commit --amend -m "Fix login crash on empty username"
```

**Scenario 2**: Wrong files in commit, not pushed

```bash
git add .
git commit -m "Add feature"  # Oops, included debug files

# Undo and redo
git reset --soft HEAD~1
git restore debug.log  # Remove unwanted file
git add .
git commit -m "Add feature"
```

**Scenario 3**: Bad commit, already pushed

```bash
git push origin main  # Pushed bad commit

# Don't reset! Revert instead
git revert HEAD
git push origin main
```

**Scenario 4**: Want to squash last 3 commits (not pushed)

```bash
git reset --soft HEAD~3
git commit -m "Combined: Feature X complete"
```

---

## 13. Rebasing

### What Rebase Does

**Simple Explanation**: Rebase moves your commits to a new starting point.

**The Problem**:

```
You started working:
main → c1 → c2
              ↘
                c3 → c4 (your branch)

Meanwhile, main got new commits:
main → c1 → c2 → c5 → c6
              ↘
                c3 → c4 (your branch)
```

**With Merge**:

```bash
git merge main

Result:
main → c1 → c2 → c5 → c6
              ↘         ↘
                c3 → c4 → c7 (merge commit)
```

**With Rebase**:

```bash
git rebase main

Result:
main → c1 → c2 → c5 → c6 → c3' → c4'
```

**Key Points**:
- c3' and c4' are NEW commits (same changes, different base)
- c3 and c4 still exist but are unreachable
- Linear history (no merge commit)

**Basic Rebase**:

```bash
# On your feature branch
git rebase main

# Or specify explicitly
git switch feature
git rebase main
```

**What Happens**:
1. Git finds common ancestor
2. Saves your commits temporarily
3. Moves branch pointer to main
4. Replays your commits one by one

**If Conflicts Occur**:

```bash
$ git rebase main
# CONFLICT in file.js

# Fix the conflict
$ nano file.js
$ git add file.js

# Continue rebase
$ git rebase --continue

# If another conflict, repeat

# Or abort entire rebase
$ git rebase --abort
```

### Interactive Rebase

**Most Powerful Git Feature**: Edit, combine, reorder commits

**Syntax**:

```bash
# Rebase last 3 commits
git rebase -i HEAD~3

# Rebase everything since branching from main
git rebase -i main
```

**Opens Editor**:

```
pick a3f5e2c Add login form
pick 7c8e9a1 Fix typo
pick 9d8c7b6 Add styles

# Commands:
# p, pick = use commit
# r, reword = use commit, but edit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like squash, but discard commit message
# d, drop = remove commit
```

**Common Operations**:

**Squash Multiple Commits**:

```
pick a3f5e2c Add login form
squash 7c8e9a1 Fix typo
squash 9d8c7b6 Add styles

# Results in ONE commit with combined message
```

**Reword Commit Message**:

```
pick a3f5e2c Add login form
reword 7c8e9a1 Fix typo
pick 9d8c7b6 Add styles

# Git will stop and let you edit the message
```

**Drop a Commit**:

```
pick a3f5e2c Add login form
drop 7c8e9a1 Fix typo
pick 9d8c7b6 Add styles

# Typo commit is removed from history
```

**Reorder Commits**:

```
pick 9d8c7b6 Add styles
pick a3f5e2c Add login form
pick 7c8e9a1 Fix typo

# Commits applied in this new order
```

**Edit a Commit**:

```
pick a3f5e2c Add login form
edit 7c8e9a1 Fix typo
pick 9d8c7b6 Add styles

# Git stops at that commit
# Make your changes
$ git add .
$ git commit --amend
$ git rebase --continue
```

**Practical Example**:

```bash
# Your messy history
$ git log --oneline
9d8c7b6 Fix bug
7c8e9a1 WIP
3a2b1c0 More work
a3f5e2c Start feature

# Interactive rebase
$ git rebase -i HEAD~4

# In editor:
pick a3f5e2c Start feature
squash 3a2b1c0 More work
squash 7c8e9a1 WIP
squash 9d8c7b6 Fix bug

# Save and close
# Git combines all into one commit
```

### Rebase vs Merge: The Decision Table

| Factor | Use Rebase | Use Merge |
|--------|-----------|-----------|
| Working alone | ✅ Yes | Either |
| Feature branch | ✅ Yes | Either |
| Shared branch | ❌ No | ✅ Yes |
| Want linear history | ✅ Yes | ❌ No |
| Want to preserve history | ❌ No | ✅ Yes |
| Public commits | ❌ No | ✅ Yes |
| Before PR | ✅ Yes | ❌ No |
| Merging PR | ❌ No | ✅ Yes |

**Golden Rules**:

1. **Never rebase commits that exist on public branches**
2. **Rebase feature branches before merging**
3. **Use merge for combining branches**

**Workflow Comparison**:

**Merge Workflow**:

```bash
# Feature branch
git switch -c feature
# ...work...
git commit -m "Add feature"

# Update from main
git merge main
# Merge commit created

# Finally
git switch main
git merge feature
```

**Rebase Workflow**:

```bash
# Feature branch
git switch -c feature
# ...work...
git commit -m "Add feature"

# Update from main
git rebase main
# Commits replayed on top of main

# Finally
git switch main
git merge feature  # Fast-forward merge
```

### The Golden Rule of Rebase

**NEVER REBASE COMMITS THAT HAVE BEEN PUSHED TO A PUBLIC/SHARED REPOSITORY**

**Why?**

```
Your branch:
c1 → c2 → c3

After you push and others pull:
Alice's repo: c1 → c2 → c3
Bob's repo:   c1 → c2 → c3

You rebase (c3 becomes c3'):
Your repo: c1 → c2 → c3'

You force push:
Origin: c1 → c2 → c3'

Alice and Bob are now in a mess:
Their c3 no longer matches origin's c3'
```

**Safe Rebase Scenarios**:

✅ **Your local feature branch** (not pushed):
```bash
git switch feature
git rebase main  # ✅ Safe
```

✅ **Your personal feature branch** (pushed, but only you use it):
```bash
git rebase main
git push --force-with-lease origin feature  # ✅ Safe if only you use it
```

❌ **Shared branch**:
```bash
git switch develop  # Multiple people use this
git rebase main  # ❌ DON'T DO THIS
```

### Practical Rebase Workflows

**Clean Up Before Creating PR**:

```bash
# You have messy commits
$ git log --oneline
a5b4c3d Fix typo
9d8c7b6 WIP save point
7c8e9a1 More progress
3a2b1c0 Start feature

# Interactive rebase to clean up
$ git rebase -i HEAD~4

# Squash into one commit
pick 3a2b1c0 Start feature
squash 7c8e9a1 More progress
squash 9d8c7b6 WIP save point
squash a5b4c3d Fix typo

# Now: clean history for PR
$ git log --oneline
1e2d3c4 Add user authentication feature
```

**Keep Feature Branch Updated**:

```bash
# Your feature branch
$ git switch feature

# Main has new commits
$ git rebase main

# If conflicts, resolve and continue
$ git add .
$ git rebase --continue

# Push (need force push if you've pushed before)
$ git push --force-with-lease origin feature
```

**Recover from Rebase Mistake**:

```bash
# Rebase went wrong
$ git rebase --abort  # If still in progress

# Or if already committed
$ git reflog
$ git reset --hard HEAD@{5}  # Go back to before rebase
```

---

## 14. Advanced Operations

### git cherry-pick

**What It Does**: Applies a specific commit from one branch to another

**Use Cases**:
- Apply a bug fix from main to a release branch
- Copy a commit from one feature to another
- Apply a teammate's commit to your branch

**Syntax**:

```bash
git cherry-pick 
```

**Example**:

```
main → c1 → c2 → c3 (contains bug fix)
         ↘
           c4 → c5 (feature branch, needs the fix)
```

```bash
# On feature branch
$ git switch feature

# Cherry-pick the bug fix
$ git cherry-pick c3

# Result:
# feature → c4 → c5 → c3' (copy of c3)
```

**Cherry-Pick Multiple Commits**:

```bash
# Pick commits c2 and c3
git cherry-pick c2 c3

# Pick range of commits
git cherry-pick c2^..c5
```

**If Conflicts**:

```bash
$ git cherry-pick a3f5e2c
# CONFLICT

$ nano file.js  # Resolve
$ git add file.js
$ git cherry-pick --continue

# Or abort
$ git cherry-pick --abort
```

**Practical Example**:

```bash
# You're on release-1.0 branch
# You need a critical fix from main

$ git log main --oneline
a3f5e2c Fix security vulnerability
7c8e9a1 Add new feature

# Pick only the security fix
$ git switch release-1.0
$ git cherry-pick a3f5e2c

# Now release-1.0 has the fix without the new feature
```

**Cherry-Pick with Custom Message**:

```bash
git cherry-pick --edit a3f5e2c
# Opens editor to modify commit message
```

### Detached HEAD State

**What It Is**: HEAD points to a commit instead of a branch

**When It Happens**:
- Checking out a specific commit
- Checking out a tag
- During rebase/cherry-pick

**Example**:

```bash
$ git checkout a3f5e2c

# Warning:
# You are in 'detached HEAD' state...
```

**Visual**:

```
Normal:
main → c1 → c2 → c3
                  ↑
                main
                  ↑
                HEAD

Detached:
main → c1 → c2 → c3
        ↑     ↑
       c2   main
        ↑
       HEAD (detached)
```

**What You Can Do**:
- Look around
- Make experimental commits
- Test old code

**What Happens to Commits in Detached HEAD**:

```bash
# In detached HEAD
$ git
