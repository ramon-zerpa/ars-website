# GitHub Connection Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Correct Git configuration, authenticate with GitHub, and push the project to a new remote repository.

**Architecture:** Use `git` for local snapshots and `gh` CLI for repository management and authentication.

**Tech Stack:** Git, GitHub CLI (gh), Windows PowerShell.

---

### Task 1: Finalize Local Identity and Repository State

**Files:**
- Modify: `.git/config` (via commands)
- Test: `git -C ars-website config --list`

**Step 1: Ensure global identity is set**
Run: `git config --global user.name "Ramon Zerpa"; git config --global user.email "elitewebve@gmail.com"`
Expected: No output, command succeeds.

**Step 2: Stage and commit all existing project files**
Run: `git -C ars-website add .`
Run: `git -C ars-website commit -m "feat: initial commit of website files"`
Expected: Commit successful with all files tracked.

---

### Task 2: Install and Authenticate GitHub CLI

**Files:**
- None (System setup)

**Step 1: Install GitHub CLI via winget**
Run: `winget install GitHub.cli`
Expected: Installation completes successfully.

**Step 2: Authentication**
Run: `gh auth login`
Note: This requires interactive input. Guide the user to select:
1. GitHub.com
2. HTTPS
3. Y (Authenticate Git with GitHub credentials)
4. Login with a web browser
Expected: User sees a code, pastes it into the browser, and logs in.

---

### Task 3: Create Remote Repository and Push

**Files:**
- Modify: `.git/config` (via `gh` commands)

**Step 1: Create a new repository on GitHub**
Run: `gh repo create ars-website --public --source=ars-website --remote=origin --push`
Expected: A new public repository created on GitHub with the local files pushed to the `master` branch.

---

### Task 4: Educational Walkthrough

**Step 1: Demonstrate Push/Pull**
1. Create a dummy file: `echo "test" > ars-website/test.txt`
2. Commit: `git -C ars-website add test.txt; git -C ars-website commit -m "docs: test commit for push demo"`
3. Push: `git -C ars-website push origin master`
Expected: Files visible on GitHub web UI.

---

### Task 5: Cleanup
**Step 1: Remove dummy file**
Run: `rm ars-website/test.txt; git -C ars-website add test.txt; git -C ars-website commit -m "cleanup: remove test file"; git -C ars-website push origin master`
Expected: Repo clean and synced.
