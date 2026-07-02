# Learning Roadmap: GitHub — Phase 1 (The Platform)

**Goal:** Become genuinely comfortable with **GitHub the platform** — not just Git — so you can host and manage repositories, collaborate through Issues/PRs/reviews, plan work with Projects, and (the QAOps payoff) automate builds, tests, and quality gates with GitHub Actions. Understand *why* each surface exists and where it fits a test-automation workflow.
**Context:** QAOps / test automation direction, plus general programming and building FE/BE apps. GitHub is where your Git work, your Cypress/Playwright suites, and your CI pipeline all come together.
**Time budget:** ~43–60 hrs of focused study + practice. No fixed weekly schedule — pace yourself; tell me your weekly hours anytime and I'll convert this to a calendar.
**Starting point:** Beginner on the platform, but **not** starting from zero — you have a Git Phase 1 plan in progress. This roadmap deliberately **does not re-teach Git or the mechanics of pushing/opening a PR** (your Git roadmap owns that). It picks up where Git ends: everything GitHub adds *on top of* Git.

---

## 🗺️ Overview

Git is version control; **GitHub is a platform built on top of Git** — hosting, collaboration, planning, automation, and governance. That one distinction organizes the whole roadmap. We start by getting oriented in the platform and its repositories (and Markdown, which powers every text surface on GitHub). Then we move through the collaboration surfaces (Issues, the PR *review* experience, Discussions), then planning (Projects, milestones, labels). The back half is the QAOps core: **GitHub Actions** — first the automation fundamentals, then real test pipelines with secrets, matrices, and artifacts. We finish on governance and security — branch protection, required status checks, Dependabot, releases — the machinery that turns "tests exist" into "a red test blocks the merge." By the end you can run a real project's collaboration, planning, and CI entirely on GitHub, and explain why each piece behaves as it does.

---

## ⚠️ How This Relates To Your Other Roadmaps (read this)

- **Git Phase 1** covers the Git *engine*: commits, branching, merging, remotes, the fetch/pull/push loop, and the *basic* mechanics of the PR workflow + GitHub flow. **Don't relearn those here.** This roadmap assumes you can already push a branch and open a PR.
- **This roadmap** covers the *platform* around that engine — the web UI, Issues, the PR **review** experience (not the git mechanics), Projects, **Actions/CI**, security, and repo governance.
- **JavaScript & Cypress roadmaps** give you the test suites. Stage 5 here is where those suites get *run in CI* — this is the "Ops" in QAOps clicking into place.
> Some light overlap on PRs is unavoidable and useful — but where it appears, the emphasis is on GitHub's UI and review features, not on `git push`.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **Git fundamentals** 🔴 — init/add/commit, branching, remotes, push, and opening a PR. This is your Git Phase 1 roadmap; you need roughly through its Stage 5 (Remotes & Collaboration). — est. **covered by your Git plan**
- [ ] **A GitHub account with 2FA enabled** 🔴 — GitHub requires two-factor auth for contributors; set it up once, now. — est. **30 min**
- [ ] **A terminal + code editor (VS Code)** 🟡 — you already have this from your other tracks. — est. **0–30 min**
> ✅ Skip any you already have. The one that actually gates you is Git — if you can't yet push a branch and open a PR, finish that side first.

---

## Stage 1: The Platform & Repositories — Getting Oriented
**Goal of this stage:** Understand what GitHub adds on top of Git, and navigate a repository fluently in the web UI — including Markdown, which powers every text surface you'll touch later.
**Estimated time:** 5–7 hrs
**Milestone:** You can create a repo (choosing visibility, README, .gitignore, license), explain each tab in the repo UI, write a clean README in GitHub-Flavored Markdown, and authenticate your local machine to GitHub (SSH or a token) — and articulate "Git does X; GitHub adds Y on top."

### Must-Know Topics 🔴
- [ ] **Git vs GitHub** — the core distinction: Git = version control engine; GitHub = hosting + collaboration + automation + governance layered on top. Everything else follows from this.
- [ ] Repositories on the platform — creating one, **visibility (public / private / internal)**, README, `.gitignore` templates, license selection, topics/description
- [ ] The repo UI — Code tab, commit history, branches & tags views, the Releases and Insights tabs; reading a repo you've never seen
- [ ] **Markdown & GitHub-Flavored Markdown (GFM)** — headings, lists, code blocks, tables, task lists, and links; this powers READMEs, Issues, PRs, and docs everywhere on GitHub
- [ ] Authenticating to GitHub — **HTTPS + Personal Access Token vs SSH keys**; why passwords alone don't work anymore

### Should-Know Topics 🟡
- [ ] The **`gh` CLI** — doing GitHub things (create repo, open PR, view runs) from the terminal; you'll appreciate it later in CI contexts
- [ ] Your **profile README** — the special `username/username` repo; a nice hands-on Markdown exercise
- [ ] GitHub Pages (light touch) — that a repo can publish a website; you'll revisit it for test reports in Stage 6

### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me the difference between Git and GitHub — what the platform adds on top of the version-control engine (hosting, collaboration, automation, governance). Quiz me until I can explain where Git ends and GitHub begins."
> 2. "Walk me through GitHub repositories and the web UI — visibility options, README/.gitignore/license, and every tab. Verify I can navigate an unfamiliar repo."
> 3. "Teach me GitHub-Flavored Markdown and how I authenticate to GitHub (SSH vs token). Quiz me on Markdown syntax and on which auth method to use when."

---

## Stage 2: Collaboration Surfaces — Issues, Reviews & Discussions
**Goal of this stage:** Use GitHub's collaboration features the way a team does — track work as Issues, run and respond to code **reviews** on PRs, and communicate through the platform. (Focus is the GitHub UI and review features, *not* the git push/branch mechanics your Git roadmap covers.)
**Estimated time:** 6–8 hrs
**Milestone:** You can file a well-structured bug report using an issue template, link it to a PR that auto-closes it, run a full review on a PR (inline comments, suggested changes, approve/request-changes), and explain when to use Issues vs Discussions.

### Must-Know Topics 🔴
- [ ] **Issues** — creating them, labels, assignees, milestones, **task lists**, and **issue templates & forms** (structured, reproducible bug reports — a QA superpower)
- [ ] **Linking issues ↔ PRs ↔ commits** — closing keywords (`Fixes #123`), cross-references, and why traceability matters
- [ ] The **PR as a review surface** — the "Files changed" view, **inline comments, suggested changes, review states (approve / request changes / comment)**, draft PRs, re-requesting review
- [ ] **Code review mechanics & etiquette on GitHub** — reviewing others' code and responding to review on your own
- [ ] Notifications, `@mentions`, and mentioning teams

### Should-Know Topics 🟡
- [ ] **Discussions vs Issues** — Q&A/ideas vs actionable work; when each fits
- [ ] **CODEOWNERS** — auto-requesting the right reviewers (you'll pair this with branch protection in Stage 6)
- [ ] Saved replies, reactions, and keeping issue threads readable

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me GitHub Issues as a work-tracking and bug-reporting tool — labels, milestones, templates/forms, and linking issues to PRs with closing keywords. Quiz me on writing a reproducible bug report."
> 2. "Teach me the pull request *review* experience on GitHub — the Files-changed view, inline comments, suggested changes, and review states. Have me role-play reviewing a PR and defending my review decisions."
> 3. "Teach me when to use Issues vs Discussions and how CODEOWNERS routes reviews. Make me decide for a few scenarios."

---

## Stage 3: Planning & Tracking — Projects, Milestones & Labels
**Goal of this stage:** Move from individual issues to an organized, trackable plan using GitHub Projects — the platform's built-in project management.
**Estimated time:** 5–7 hrs
**Milestone:** You can build a Project with table + board + roadmap views, add custom fields (priority, status, an iteration), automate it so merged PRs move items to Done, and run a small triage workflow — e.g. a QA/test-cycle board.

### Must-Know Topics 🔴
- [ ] **GitHub Projects** (the current Projects) — adding issues/PRs, and the three layouts: **table, board (kanban), and roadmap**
- [ ] **Custom fields** — status, priority, estimate, and **iteration fields** for sprint-style planning
- [ ] Views — filtering, sorting, grouping, and saving multiple views for different angles
- [ ] **Milestones & labels** — grouping work toward a target and categorizing it (bug/enhancement/triage)

### Should-Know Topics 🟡
- [ ] **Built-in Project automations** — auto-add items, set status on merge, auto-archive; connecting planning to actual code events
- [ ] **Sub-issues & issue dependencies** — breaking down large work and marking what blocks what
- [ ] **Project insights/charts** — burn-up, velocity, and custom charts for a QA dashboard

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me GitHub Projects — table, board, and roadmap views, custom fields, and iteration planning. Verify I can design a board for tracking a QA test cycle."
> 2. "Teach me milestones, labels, and Project automations that react to issue/PR events. Quiz me on wiring a triage-to-done workflow."

---

## Stage 4: GitHub Actions I — Automation Fundamentals
**Goal of this stage:** Understand the Actions mental model and get a real CI workflow running tests on every push and PR. This is the gateway to QAOps.
**Estimated time:** 7–9 hrs
**Milestone:** You can explain the events → workflows → jobs → steps → actions model, write a workflow YAML from scratch that checks out code, installs dependencies, and runs a test suite, and see its status check appear on a PR — and read the logs when it fails.

### Must-Know Topics 🔴
- [ ] **The Actions model** — **events trigger workflows; workflows contain jobs; jobs run steps on runners; steps `run` commands or `use` actions.** Get this hierarchy solid.
- [ ] **Runners** — GitHub-hosted VMs (Ubuntu/Windows/macOS); jobs run in fresh, isolated environments
- [ ] **Workflow YAML anatomy** — the `.github/workflows/` directory, `name`, `on:`, `jobs:`, `runs-on:`, `steps:`
- [ ] **Triggers (`on:`)** — `push`, `pull_request`, `workflow_dispatch` (manual), `schedule` (cron); which to use when
- [ ] **Using actions from the Marketplace** — `uses: actions/checkout@v4`, `uses: actions/setup-node@v4`, plus `run:` shell steps
- [ ] **Your first CI workflow** — checkout → setup runtime → install → **run tests**; watching it as a **status check on the PR**

### Should-Know Topics 🟡
- [ ] The **Actions tab** — run history, re-running failed jobs, reading logs, workflow syntax errors
- [ ] **Starter workflow templates** — GitHub's preconfigured CI templates as a launch pad
- [ ] Basic **contexts & expressions** — `${{ github.event_name }}` and friends (light introduction)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the GitHub Actions mental model — events, workflows, jobs, steps, actions, runners — and the anatomy of a workflow YAML file. Quiz me on what runs where and in what order."
> 2. "Walk me through writing a first CI workflow that runs my test suite on push and pull_request, and show me how it becomes a status check on the PR. Give me broken YAML to debug."

---

## Stage 5: GitHub Actions II — Real Test Pipelines (QAOps Core) 🧠
**Goal of this stage:** This is the QAOps payoff stage. Turn a toy CI workflow into a real test pipeline — with secrets, dependency caching, cross-version matrices, and uploaded test artifacts — the exact setup that runs your Cypress/Playwright suites in the cloud.
**Estimated time:** 10–14 hrs (slow down — this is where your testing tracks and GitHub converge)
**Milestone:** You can run a browser/API test suite in Actions with cached dependencies, a **matrix** across Node versions (or browsers/OSes), **secrets** injected safely, and **test reports + screenshots/videos uploaded as artifacts** on failure — and explain each choice.

### Must-Know Topics 🔴
- [ ] **Secrets & variables** — repository/environment secrets, `${{ secrets.X }}`, and env vars; never hardcode credentials in a workflow
- [ ] **`GITHUB_TOKEN` & permissions** — the auto-provided token and the **principle of least privilege** (`permissions:`)
- [ ] **Caching dependencies** — `actions/cache` and setup-node's built-in cache; why it makes CI dramatically faster
- [ ] **Matrix builds** — running the same job across multiple Node versions / OSes / browsers in parallel (cross-environment test coverage)
- [ ] **Artifacts** — `actions/upload-artifact` for test reports, **screenshots and videos on failure** (the tester's black box)
- [ ] **Running a real E2E suite in CI** — wiring your Cypress/Playwright suite into a workflow (ties directly to your other roadmaps)

### Should-Know Topics 🟡
- [ ] **Job dependencies & concurrency** — `needs:` for sequencing (lint → test → build), `concurrency:` to cancel stale runs and save minutes
- [ ] **Test reporting** — JUnit/HTML reporters surfaced in CI, and status **badges** in your README
- [ ] **Reusable & composite workflows** — `workflow_call` and composite actions to avoid copy-paste across repos (introduction)
- [ ] **Self-hosted runners** — what they are and when a team reaches for them (awareness, not depth)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me secrets, variables, and GITHUB_TOKEN permissions in GitHub Actions. Quiz me on how to inject credentials safely and apply least privilege."
> 2. "Teach me dependency caching and matrix builds in Actions — running tests across multiple Node versions/OSes. Verify I understand why caching and matrices matter for a test suite."
> 3. "Teach me uploading test artifacts — reports, screenshots, videos on failure — and wiring a real Cypress/Playwright E2E suite into a CI workflow. Have me design the pipeline end to end."

---

## Stage 6: Governance, Security & Releases — Shipping Safely
**Goal of this stage:** Put quality gates and guardrails around the repo — the machinery that makes CI *enforceable* — plus platform security features and releases. This is where "we have tests" becomes "you cannot merge past a failing test."
**Estimated time:** 8–11 hrs
**Milestone:** You can protect `main` with a ruleset that **requires a passing CI status check and a review before merge**, explain the collaborator permission levels, enable and interpret Dependabot/secret scanning, and cut a tagged release (bonus: automated via Actions).

### Must-Know Topics 🔴
- [ ] **Branch protection / repository rulesets** — require a PR, **require passing status checks** (your Stage 5 CI as a merge gate), require reviews/approvals, require linear history; *why a red test blocks the merge*
- [ ] **Collaborator roles & permissions** — read / triage / write / maintain / admin; teams and a light intro to organizations
- [ ] **Platform security features** — **Dependabot** alerts & version updates, **secret scanning & push protection**, and **code scanning (CodeQL)** as an intro; running these as part of CI
- [ ] **Releases & tags on the platform** — creating a release, release notes, attaching assets; how this differs from a bare git tag

### Should-Know Topics 🟡
- [ ] **Automating releases** with Actions (tag → build → publish release)
- [ ] **GitHub Pages for test reports/docs** — publishing an HTML report or coverage site straight from a repo
- [ ] **Required status checks + CODEOWNERS together** — a complete quality-gate setup for a team

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me branch protection and repository rulesets — requiring passing status checks and reviews before merge — and collaborator permission levels. Quiz me on designing a quality gate for a team's main branch."
> 2. "Teach me GitHub's built-in security features — Dependabot, secret scanning/push protection, and code scanning — and how they run in CI. Verify I can interpret and act on an alert."
> 3. "Teach me releases and tags on GitHub and how to automate a release with Actions. Connect it to a QAOps shipping workflow."

---

## 🏁 Final Milestone
You can run a real project entirely on GitHub: a well-structured repo with a clear README, work tracked as Issues on a Project board, PRs reviewed through GitHub's review tools, a **GitHub Actions CI pipeline that runs your test suite** (cached, matrixed, with artifacts on failure) on every push and PR, and a **protected `main` branch where a failing test blocks the merge** — plus Dependabot and secret scanning watching your back and tagged releases marking versions. And you can explain, to another engineer, *why* each of these platform features exists and how it fits a QAOps strategy.

---

## ⏭️ What's Out of Scope (For Now)
- **Deep Git mechanics** — owned by your Git Phase 1 roadmap; not repeated here.
- **Org / Enterprise administration at scale** (SSO/SAML, audit logs, enterprise policy) — relevant once you're an admin, not a contributor. A Phase 2 topic.
- **Writing custom Actions from scratch** (JavaScript or Docker actions) — advanced; you'll *use* Marketplace actions here, not author your own yet.
- **GitHub REST & GraphQL APIs, webhooks, and GitHub Apps** — powerful automation, but a separate Phase 2 track (great "next" once Actions clicks).
- **Codespaces (cloud dev environments)** — useful, not foundational; revisit after the core platform.
- **GitHub Copilot / AI features** — a distinct track; deliberately excluded to keep the platform focus.
- **Full continuous *deployment* to cloud providers (AWS/Vercel/etc.)** — you'll touch CD lightly in Actions; production deployment pipelines are their own roadmap.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Git vs GitHub: "Teach me the difference between Git and GitHub — what the platform adds on top of the version-control engine. Quiz me until I can explain where Git ends and GitHub begins."
2. Stage 1 — Repos/UI: "Walk me through GitHub repositories and the web UI — visibility, README/.gitignore/license, and every tab. Verify I can navigate an unfamiliar repo."
3. Stage 1 — Markdown/auth: "Teach me GitHub-Flavored Markdown and authenticating to GitHub (SSH vs token). Quiz me on Markdown syntax and which auth method to use when."
4. Stage 2 — Issues: "Teach me GitHub Issues as a work-tracking and bug-reporting tool — labels, milestones, templates/forms, linking to PRs with closing keywords. Quiz me on writing a reproducible bug report."
5. Stage 2 — Reviews: "Teach me the PR *review* experience — Files-changed, inline comments, suggested changes, review states. Have me role-play reviewing a PR."
6. Stage 2 — Discussions/CODEOWNERS: "Teach me Issues vs Discussions and how CODEOWNERS routes reviews. Make me decide for a few scenarios."
7. Stage 3 — Projects: "Teach me GitHub Projects — table, board, roadmap views, custom fields, iterations. Verify I can design a QA test-cycle board."
8. Stage 3 — Milestones/automation: "Teach me milestones, labels, and Project automations that react to issue/PR events. Quiz me on a triage-to-done workflow."
9. Stage 4 — Actions model: "Teach me the GitHub Actions mental model — events, workflows, jobs, steps, actions, runners — and workflow YAML anatomy. Quiz me on what runs where and in what order."
10. Stage 4 — First CI: "Walk me through a first CI workflow that runs my tests on push and pull_request, appearing as a status check. Give me broken YAML to debug."
11. Stage 5 — Secrets/permissions: "Teach me secrets, variables, and GITHUB_TOKEN permissions. Quiz me on injecting credentials safely with least privilege."
12. Stage 5 — Caching/matrix: "Teach me dependency caching and matrix builds — running tests across Node versions/OSes. Verify I understand why they matter for a test suite."
13. Stage 5 — Artifacts/E2E: "Teach me uploading test artifacts (reports, screenshots, videos on failure) and wiring a real Cypress/Playwright suite into CI. Have me design the pipeline."
14. Stage 6 — Governance: "Teach me branch protection/rulesets — requiring passing checks and reviews before merge — and permission levels. Quiz me on designing a quality gate for main."
15. Stage 6 — Security: "Teach me Dependabot, secret scanning/push protection, and code scanning, and how they run in CI. Verify I can act on an alert."
16. Stage 6 — Releases: "Teach me releases and tags on GitHub and automating a release with Actions. Connect it to a QAOps shipping workflow."
