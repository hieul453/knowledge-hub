# Learning Roadmap: Git — Phase 1 (Team Collaboration)
 
**Goal:** Become genuinely comfortable with Git for everyday development — confidently track work, branch, collaborate via pull requests, recover from mistakes, and understand how Git underpins a test-automation / CI pipeline.
**Context:** Foundation for QAOps / test automation, general programming, and building full-stack (FE/BE) apps.
**Time budget:** No fixed schedule — estimates are in hours so you can pace yourself.
**Starting point:** Total beginner. No prior Git experience assumed.
 
---
 
## 🗺️ Overview
 
We start by building the *right mental model* — what Git actually stores (snapshots, not diffs) and the three places your work lives. From there it's relentlessly practical: the daily commit loop, branching and merging, the "undo my mistake" safety net, then collaboration through remotes and pull requests. We finish on the workflows that matter for shipping and testing — branching strategies, tags/releases, and how Git events drive CI pipelines. By the end you won't just memorize commands; you'll know *why* each one does what it does.
 
**Total estimated time:** ~26–34 hours of focused study + practice (add your own reps on a real project).
 
---
 
## Prerequisites (Complete Before Stage 1)
 
- [ ] **Basic command line** — navigate directories (`cd`, `ls`/`dir`), create/edit files, run a command — est. 1–2 hrs
- [ ] **A code editor installed** (VS Code is fine) and a terminal you're comfortable opening — est. 30 min
> ✅ Skip if you already work in a terminal day to day. If unsure, skim and move on — you'll pick the rest up as you go.
 
---
 
## Stage 1: Mental Model & Setup — Foundation
**Goal of this stage:** Understand what Git *is* and what it stores, and get a working, configured install.
**Estimated time:** ~3–4 hours
**Milestone:** You can explain in your own words what a commit is, what the staging area is for, and you have Git installed with your name/email configured.
 
### Must-Know Topics 🔴
- [ ] What version control is and why it exists — the problem Git solves
- [ ] Git's data model: a commit is a **snapshot**, not a diff; commits link to parents to form history
- [ ] The three areas: **working directory → staging area (index) → repository**
- [ ] Install Git; configure `user.name`, `user.email`, default branch, editor
- [ ] Start a repo: `git init` vs `git clone`
### Should-Know Topics 🟡
- [ ] What a SHA / commit hash is and why content-addressing matters (light touch — builds intuition for later recovery work)
- [ ] How `HEAD` points at "where you are now"
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me Git's data model — why a commit is a snapshot not a diff, and how the working directory, staging area, and repository relate. Quiz me until I can explain it without notes."
> 2. "Walk me through setting up Git from scratch and the difference between `git init` and `git clone`, then verify I understand what each created."
 
---
 
## Stage 2: The Daily Loop — Tracking Work
**Goal of this stage:** Run the everyday cycle fluently and read your own history.
**Estimated time:** ~3–4 hours
**Milestone:** You can take any folder, track it, make a series of clean commits, inspect what changed, and ignore the right files — without looking up commands.
 
### Must-Know Topics 🔴
- [ ] `git status` — your most-used command; read it like a dashboard
- [ ] `git add` (stage), `git commit` — the core loop
- [ ] `git diff` (working vs staged vs committed) — see exactly what changed
- [ ] `git log` and its useful flags (`--oneline`, `--graph`, `--all`)
- [ ] `.gitignore` — keep build artifacts, secrets, `node_modules`, logs out of history (critical for clean test repos)
### Should-Know Topics 🟡
- [ ] Writing good commit messages (why small, focused commits pay off later in `bisect` and code review)
- [ ] `git show` to inspect a single commit
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the daily Git loop — status, add, diff, commit, log — and drill me with scenarios where I have to predict what `git status` will show."
> 2. "Teach me `.gitignore` and what should never be committed, especially for a test-automation / app project. Quiz me on edge cases like already-tracked files."
 
---
 
## Stage 3: Branching & Merging — Parallel Work
**Goal of this stage:** Work on isolated branches and integrate them, including resolving conflicts calmly.
**Estimated time:** ~5–6 hours
**Milestone:** You can create a feature branch, do work, merge it back, and resolve a merge conflict without panic. You can articulate when to merge vs rebase.
 
### Must-Know Topics 🔴
- [ ] Branches as cheap movable pointers — `git branch`, `git switch` / `git checkout`
- [ ] Fast-forward vs 3-way merge — `git merge`
- [ ] **Merge conflicts** — what they look like, how to resolve, how to abort
- [ ] Rebase basics — `git rebase`, and *why* it produces linear history
### Should-Know Topics 🟡
- [ ] The "Golden Rule of Rebasing": don't rebase shared/public history
- [ ] Interactive rebase (`rebase -i`) preview — squash, reorder (you'll use this in Stage 4)
- [ ] Deleting and renaming branches
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Git branching and merging using the mental model that a branch is just a pointer. Quiz me on what the commit graph looks like after each operation."
> 2. "Teach me merge conflicts end to end — why they happen, how to read the conflict markers, resolve, and abort. Give me practice scenarios."
> 3. "Teach me merge vs rebase — the trade-offs, the Golden Rule, and when a team would pick each. Make sure I can justify a choice."
 
---
 
## Stage 4: Undo & Recovery — The Safety Net
**Goal of this stage:** Fix mistakes confidently. This is the stage that turns Git from scary into a superpower.
**Estimated time:** ~5–6 hours
**Milestone:** Given a described mistake (wrong branch, bad commit, lost work, accidental `reset --hard`), you can pick the correct recovery command and explain why it's safe or destructive.
 
### Must-Know Topics 🔴
- [ ] `git restore` / `git checkout --` — discard working changes, unstage
- [ ] `git commit --amend` — fix the last commit
- [ ] `git reset` — `--soft` vs `--mixed` vs `--hard` and what each moves
- [ ] `git revert` — undo safely on shared history (creates a new commit)
- [ ] `git reflog` — the time machine; recover "lost" commits and deleted branches
### Should-Know Topics 🟡
- [ ] `git stash` — park work-in-progress, switch contexts, restore
- [ ] Recovering a deleted branch via reflog
- [ ] When a change is *truly* unrecoverable (uncommitted + discarded)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Git's undo toolkit — restore, amend, reset (all three modes), revert. Drill me on choosing the right one for a given mistake and which are destructive."
> 2. "Teach me `git reflog` and recovery — how to get back lost commits and deleted branches. Give me 'I broke it, fix it' scenarios."
> 3. "Teach me `git stash` and when to reach for it versus a quick commit."
 
---
 
## Stage 5: Remotes & Collaboration — Working With Others
**Goal of this stage:** Push/pull with a remote and collaborate through the pull request workflow.
**Estimated time:** ~5–6 hours
**Milestone:** You can clone a remote, push a feature branch, open a pull request, respond to review, and merge — and you understand fetch vs pull.
 
### Must-Know Topics 🔴
- [ ] Remotes — `git remote`, `origin`, `git clone`
- [ ] `git fetch` vs `git pull` (and why the distinction matters)
- [ ] `git push`, tracking branches, upstream
- [ ] The pull request (PR) workflow: branch → push → PR → review → merge
- [ ] GitHub flow as a concrete, lightweight team model
### Should-Know Topics 🟡
- [ ] Forks vs branches (open-source contribution model)
- [ ] Keeping a branch up to date with `main` (merge vs rebase, force-push caveats)
- [ ] Resolving conflicts that surface during a PR
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Git remotes — clone, fetch vs pull, push, tracking branches. Quiz me on what's local vs remote at each step."
> 2. "Teach me the pull request workflow and GitHub flow end to end, including code review and keeping my branch current. Verify I can run the full loop."
 
---
 
## Stage 6: Professional & QAOps Workflows — Shipping & Testing
**Goal of this stage:** Connect Git to how real teams ship and test — branching strategies, releases, and CI triggers.
**Estimated time:** ~5–6 hours
**Milestone:** You can describe how a CI/test pipeline hooks into Git events, choose a branching strategy for a team, and use tags and `bisect` purposefully.
 
### Must-Know Topics 🔴
- [ ] Branching strategies: GitHub flow vs trunk-based development — trade-offs
- [ ] Tags & releases — `git tag`, annotated vs lightweight, marking versions
- [ ] **Git events that drive CI** — how `push` and `pull_request` trigger automated test runs (the heart of QAOps)
- [ ] `git bisect` — binary-search history to find the commit that introduced a regression (a tester's best friend)
### Should-Know Topics 🟡
- [ ] Git hooks (`pre-commit`, `pre-push`) — run linters/tests locally before code leaves your machine
- [ ] `.gitattributes` — line endings, diff behavior, large files
- [ ] Protected branches & required status checks (why a red test blocks a merge)
### Nice-to-Know Topics 🟢
- [ ] Submodules / monorepo basics (situational)
- [ ] `git worktree` for parallel checkouts (handy for running test suites on multiple branches)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me branching strategies — GitHub flow vs trunk-based — and how each interacts with CI. Quiz me on which fits a given team."
> 2. "Teach me how Git events trigger CI test pipelines, and walk me through tags/releases. Connect it to QAOps practice."
> 3. "Teach me `git bisect` and Git hooks as testing tools. Give me a regression-hunting scenario to solve."
 
---
 
## 🏁 Final Milestone
 
You can take a project from empty folder to a collaborative, CI-tested codebase: initialize it, commit cleanly, branch for features, open and review pull requests, recover from any mistake, tag releases, and explain exactly how each push triggers the automated test suite. You can reason about *why* a Git operation behaves the way it does, not just recite the command.
 
---
 
## ⏭️ What's Out of Scope (For Now)
 
- **Git internals at the plumbing level** (`git cat-file`, object packing, the `.git` directory layout) — fascinating, but you only need the snapshot mental model to be productive. Revisit if you ever want true mastery.
- **Advanced rewriting** (`filter-repo`, removing secrets from history) — situational; learn it the day you need it.
- **Submodules / large-monorepo tooling** — only if a project forces it on you.
- **GUI clients** (Sourcetree, GitKraken) — fine to use, but learn the CLI first so you understand what the buttons do.
---
 
## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Data model: "Teach me Git's data model — why a commit is a snapshot not a diff, and how the working directory, staging area, and repository relate. Quiz me until I can explain it without notes."
2. Stage 1 — Setup: "Walk me through setting up Git from scratch and the difference between `git init` and `git clone`, then verify I understand what each created."
3. Stage 2 — Daily loop: "Teach me the daily Git loop — status, add, diff, commit, log — and drill me with scenarios where I have to predict what `git status` will show."
4. Stage 2 — gitignore: "Teach me `.gitignore` and what should never be committed, especially for a test-automation / app project. Quiz me on edge cases like already-tracked files."
5. Stage 3 — Branching: "Teach me Git branching and merging using the mental model that a branch is just a pointer. Quiz me on what the commit graph looks like after each operation."
6. Stage 3 — Conflicts: "Teach me merge conflicts end to end — why they happen, how to read the markers, resolve, and abort. Give me practice scenarios."
7. Stage 3 — Merge vs rebase: "Teach me merge vs rebase — the trade-offs, the Golden Rule, and when a team would pick each. Make sure I can justify a choice."
8. Stage 4 — Undo toolkit: "Teach me Git's undo toolkit — restore, amend, reset (all three modes), revert. Drill me on choosing the right one and which are destructive."
9. Stage 4 — Reflog/recovery: "Teach me `git reflog` and recovery — how to get back lost commits and deleted branches. Give me 'I broke it, fix it' scenarios."
10. Stage 4 — Stash: "Teach me `git stash` and when to reach for it versus a quick commit."
11. Stage 5 — Remotes: "Teach me Git remotes — clone, fetch vs pull, push, tracking branches. Quiz me on what's local vs remote at each step."
12. Stage 5 — PR workflow: "Teach me the pull request workflow and GitHub flow end to end, including code review and keeping my branch current. Verify I can run the full loop."
13. Stage 6 — Strategies/CI: "Teach me branching strategies — GitHub flow vs trunk-based — and how each interacts with CI. Quiz me on which fits a given team."
14. Stage 6 — CI triggers/releases: "Teach me how Git events trigger CI test pipelines, and walk me through tags/releases. Connect it to QAOps practice."
15. Stage 6 — Bisect/hooks: "Teach me `git bisect` and Git hooks as testing tools. Give me a regression-hunting scenario to solve."