# Learning Roadmap: Cypress — Phase 1
 
**Goal:** Understand Cypress *deeply* — not just copy-paste working tests, but know **why** it behaves the way it does (its async model, retry-ability, architecture) — so you can author and reason about automated tests with confidence.
**Context:** QAOps / test automation direction, plus general programming and building FE/BE apps. Cypress is your entry point into automated testing.
**Time budget:** ~90–125 hrs total, honestly. Roughly **40–60 hrs of prerequisites** (you're a total beginner, and Cypress tests *are* JavaScript running in a real browser) + **~50–65 hrs of Cypress itself**. Adjustable — tell me your weekly hours and I'll convert this to a calendar.
**Starting point:** Total beginner. No JS, no web, no testing background assumed.
 
---
 
## 🗺️ Overview
 
Cypress is a JavaScript end-to-end (E2E) test framework that runs **inside the browser, alongside your app** — that single architectural fact explains almost everything that makes it different. But you can't understand that fact without first understanding JavaScript, the DOM, HTTP, and what testing even *is*. So this roadmap front-loads a real foundation, then builds Cypress from its mental model (async command queue + retry-ability) outward to a CI-integrated QAOps suite. We end where your goal points: Cypress running in a pipeline, and an honest map of where Cypress stops and you reach for something else.
 
---
 
## ⚠️ A Note On Your Starting Point (read this)
 
You said "total beginner" and "understand it deeply." Those two together mean the prerequisites below are **not optional or skippable** — they're the bulk of the "deep" you asked for. Most people who find Cypress confusing (variables don't work, tests are "flaky," `.then()` is mysterious) are actually missing **JavaScript async** and **DOM** fundamentals, not Cypress knowledge. Investing in the prereqs is the single highest-leverage thing you can do. I've flagged the must-knows; don't let yourself skip them.
 
---
 
## Prerequisites (Complete Before Stage 1)
 
- [ ] **JavaScript fundamentals** 🔴 — variables, functions, objects, arrays, ES6 (arrow functions, destructuring, template literals), and especially **callbacks, Promises, and `async`/`await`**. Cypress tests are literally JS files; its whole command model is a reaction to JS async. — est. **25–40 hrs**
- [ ] **The web platform** 🔴 — what the **DOM** is, HTML structure, **CSS selectors** (you'll select elements constantly), and how a browser loads/renders a page. — est. **8–12 hrs**
- [ ] **HTTP basics** 🔴 — request/response, methods (GET/POST), status codes, JSON. You'll stub and assert on network calls. — est. **3–5 hrs**
- [ ] **Node.js & npm** 🟡 — installing packages, `package.json`, running npm scripts from a terminal. Cypress installs via npm and runs on Node. — est. **2–4 hrs**
- [ ] **Testing concepts** 🔴 — unit vs integration vs E2E, the **test pyramid**, what an assertion is, and *why* we automate tests. Grounds every decision later. — est. **3–4 hrs**
> ✅ Skip any you genuinely already know. If unsure about JS async specifically — **don't skip it.** It's the one that bites everyone.
 
---
 
## Stage 1: How Cypress Actually Works — Architecture & First Test
**Goal of this stage:** Be able to explain, in plain language, what makes Cypress different from older tools (Selenium/WebDriver) and why it runs in the browser — and get a first test passing.
**Estimated time:** 6–8 hrs
**Milestone:** You can install Cypress, run a test in both `open` and `run` modes, explain the project structure, and articulate "Cypress runs in the same run-loop as my app, which is why it can do X."
 
### Must-Know Topics 🔴
- [ ] Cypress's architecture — runs *inside* the browser alongside the app (not driving it remotely over a wire) — this is the root cause of everything else
- [ ] Install + project setup (`npm i cypress`, `npx cypress open`), spec file location, `cypress.config.js`
- [ ] `open` mode (interactive runner, time-travel debugging) vs `run` mode (headless)
- [ ] Anatomy of a test: `describe` / `it`, `cy.visit()`, a first `cy.get().click()`
### Should-Know Topics 🟡
- [ ] E2E vs Component testing — what each is for (you'll go deep on component testing in Stage 5)
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me Cypress's architecture — how it runs in the browser alongside the app, and contrast it with Selenium/WebDriver. Quiz me on *why* this matters."
> 2. "Walk me through installing Cypress and the anatomy of a first test (`describe`/`it`/`cy.visit`/`cy.get`). Make sure I can explain the project structure."
 
---
 
## Stage 2: Core Commands — Selecting, Interacting, Asserting
**Goal of this stage:** Confidently find elements, interact with them, and assert on results using resilient patterns.
**Estimated time:** 8–10 hrs
**Milestone:** You can write a multi-step test against a real form/page using `data-*` selectors, interact (type/click/select), and assert — and explain why your selectors are resilient.
 
### Must-Know Topics 🔴
- [ ] Selecting elements: `cy.get()`, `cy.contains()`, and **why `data-cy` / `data-test` attributes** beat CSS/id/class selectors
- [ ] Interacting: `.click()`, `.type()`, `.check()`, `.select()`, `.clear()`
- [ ] Assertions: `.should()` / `.and()`, implicit vs explicit assertions, the Chai vocabulary (`be.visible`, `have.text`, `have.length`)
### Should-Know Topics 🟡
- [ ] Traversal: `.find()`, `.within()`, `.first()`, `.eq()`
- [ ] Aliases: `.as()` and `cy.get('@alias')`
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me element selection in Cypress — `cy.get` vs `cy.contains` — and drill me on why `data-*` selectors are the best practice and which selectors are anti-patterns."
> 2. "Teach me Cypress assertions: implicit vs explicit, `.should()`/`.and()`, and the common Chai matchers. Quiz me by giving me a UI behavior and asking me to write the assertion."
 
---
 
## Stage 3: The Mental Model — Async, the Command Queue & Retry-ability 🧠
**Goal of this stage:** This is the *deep understanding* stage. Internalize why Cypress commands are not Promises, why you can't store them in variables, why `.then()` exists, and how retry-ability eliminates most "waiting."
**Estimated time:** 8–12 hrs (slow down here — this is the payoff for "deeply")
**Milestone:** You can correctly predict whether a given chain will retry or not, explain why `const el = cy.get(...)` is broken, and explain when you genuinely need `.then()` vs when retry-ability already handles it.
 
### Must-Know Topics 🔴
- [ ] Commands are **enqueued, not executed immediately** — they run after your test function returns
- [ ] Why Cypress chains **look** synchronous but aren't, and why they're **not Promises** (no `async`/`await` inside tests)
- [ ] **Retry-ability**: queries retry the whole chain; assertions are retry boundaries; non-query commands run once
- [ ] Why you can't assign command return values to variables (use **aliases / closures** instead)
- [ ] `.then()` — what it does, and when you actually need it
### Should-Know Topics 🟡
- [ ] The "detached from DOM" error and why mid-chain assertions can cause it
- [ ] Default timeouts and per-command timeout overrides
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the asynchronous nature of Cypress — the command queue, why commands aren't Promises, and why I can't use variables or `async`/`await`. Quiz me hard with code snippets and ask me to predict behavior."
> 2. "Teach me Cypress retry-ability in depth: what retries, what doesn't, assertions as retry boundaries. Give me flaky-looking tests and ask me to explain why they fail and fix them."
 
---
 
## Stage 4: Controlling the World — Network & Test Data
**Goal of this stage:** Take control of the network and app state so tests are fast, deterministic, and not dependent on flaky backends.
**Estimated time:** 8–10 hrs
**Milestone:** You can stub an API response with `cy.intercept`, wait on it correctly (no arbitrary `cy.wait(3000)`), seed state via `cy.request`, and load data from a fixture.
 
### Must-Know Topics 🔴
- [ ] `cy.intercept()` — spying on and **stubbing** network requests; aliasing requests and `cy.wait('@alias')`
- [ ] Why **arbitrary `cy.wait(ms)` is an anti-pattern** and what to do instead
- [ ] Fixtures — `cy.fixture()` for canned test data
- [ ] `cy.request()` — hitting the backend directly for setup/teardown and programmatic login
### Should-Know Topics 🟡
- [ ] `cy.session()` for caching login across tests
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `cy.intercept` — spying vs stubbing network requests, aliasing, and waiting on requests properly. Quiz me on why fixed `cy.wait(ms)` is bad and how to replace it."
> 2. "Teach me controlling test state: `cy.request` for setup/teardown and programmatic login vs logging in through the UI. Make me argue the trade-offs."
 
---
 
## Stage 5: Structuring a Real Suite — Patterns, Isolation & Component Testing
**Goal of this stage:** Move from "tests that pass" to "a suite that scales and survives refactors."
**Estimated time:** 10–14 hrs
**Milestone:** You can structure a multi-spec suite with custom commands, explain the Page Object vs App Actions debate and pick deliberately, keep tests isolated, and write a component test.
 
### Must-Know Topics 🔴
- [ ] Custom commands (`Cypress.Commands.add`) and the support file
- [ ] **Test isolation** — independent tests, `beforeEach` for setup, why tests must not depend on each other
- [ ] **Page Object Model vs App Actions** — the well-known debate; understand *why* the Cypress community leans toward App Actions, and when POM is still fine
- [ ] Config & environment: `baseUrl`, env variables, multiple environments
### Should-Know Topics 🟡
- [ ] **Component testing** — mounting a single component in isolation vs full E2E; when to use which
- [ ] Hooks lifecycle (`before`/`beforeEach`/`after`/`afterEach`) and gotchas
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me how to structure a Cypress suite: custom commands, test isolation, and the Page Object vs App Actions debate. Make me defend a choice for a given scenario."
> 2. "Teach me Cypress component testing vs E2E — what each tests, the trade-offs, and when to reach for each."
 
---
 
## Stage 6: QAOps — CI, Parallelization & Knowing Cypress's Limits
**Goal of this stage:** Put Cypress where your goal points — into a pipeline — and understand its boundaries as an engineer, not a fanboy.
**Estimated time:** 8–12 hrs
**Milestone:** You can run Cypress in GitHub Actions, parallelize a suite, configure retries/screenshots/videos for CI, and give a reasoned answer to "Cypress or Playwright for this project?"
 
### Must-Know Topics 🔴
- [ ] Running in CI — `cypress run` headless, the official Cypress GitHub Action
- [ ] **Parallelization** & load-balancing specs across machines (and that this needs Cypress Cloud or a third-party orchestrator)
- [ ] CI ergonomics: test retries on CI, screenshots & videos on failure, artifacts
- [ ] **Cypress's limits** — single browser/origin model, no native multi-tab, when Playwright/Selenium fit better; where Cypress sits in a QAOps strategy
### Should-Know Topics 🟡
- [ ] Cypress Cloud — analytics, flake detection, test insights
- [ ] Reporting (e.g. JUnit/mochawesome) for pipeline dashboards
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me running Cypress in CI with GitHub Actions and parallelizing the suite. Quiz me on what parallelization requires and the retries/artifacts config for CI."
> 2. "Teach me the limits of Cypress — single-origin/multi-tab constraints — and give me a framework for choosing Cypress vs Playwright for a given QAOps scenario."
 
---
 
## 🏁 Final Milestone
You can build a CI-integrated Cypress suite for a real app from scratch — resilient selectors, stubbed network, isolated tests, custom commands, running in parallel in GitHub Actions — **and** explain, to another engineer, *why* every Cypress mechanism behaves the way it does (the async queue, retry-ability, in-browser architecture) and where Cypress is the wrong tool.
 
---
 
## ⏭️ What's Out of Scope (For Now)
- **TypeScript with Cypress** — valuable, but add it once the JS + Cypress model is solid (it's a layer on top, not a foundation).
- **Visual regression / accessibility testing** (Applitools, axe, Cypress Accessibility) — specialized; revisit after the core suite.
- **BDD / Cucumber syntax** — a style choice, not a fundamental; the community is split on its value.
- **Deep Cypress plugin authoring** — advanced; not needed for your goal yet.
- **Playwright itself** — you'll *compare* against it in Stage 6, but learning it is a separate roadmap (a strong "next" once Cypress clicks).
---
 
## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Prereqs — (use external courses first; see sources file). Then: "Quiz me on JavaScript async — callbacks, Promises, async/await — until I can predict execution order reliably."
2. Stage 1 — Architecture: "Teach me Cypress's architecture — how it runs in the browser alongside the app, vs Selenium/WebDriver. Quiz me on why it matters."
3. Stage 1 — First test: "Walk me through installing Cypress and the anatomy of a first test. Make sure I can explain the project structure."
4. Stage 2 — Selectors: "Teach me element selection — `cy.get` vs `cy.contains` — and drill me on `data-*` best practice vs anti-patterns."
5. Stage 2 — Assertions: "Teach me Cypress assertions: implicit vs explicit, `.should`/`.and`, common Chai matchers. Quiz me by behavior."
6. Stage 3 — Async model: "Teach me the asynchronous nature of Cypress — command queue, not-Promises, no variables/async-await. Quiz me hard with snippets."
7. Stage 3 — Retry-ability: "Teach me retry-ability in depth: what retries, what doesn't, assertions as boundaries. Give me flaky tests to fix."
8. Stage 4 — Network: "Teach me `cy.intercept` — spying vs stubbing, aliasing, waiting properly. Quiz me on why fixed waits are bad."
9. Stage 4 — State: "Teach me `cy.request` for setup/teardown and programmatic login vs UI login. Make me argue the trade-offs."
10. Stage 5 — Structure: "Teach me suite structure: custom commands, test isolation, Page Object vs App Actions. Make me defend a choice."
11. Stage 5 — Component testing: "Teach me component testing vs E2E — trade-offs and when to use each."
12. Stage 6 — CI: "Teach me running Cypress in GitHub Actions and parallelizing. Quiz me on what parallelization requires and CI config."
13. Stage 6 — Limits: "Teach me the limits of Cypress and give me a framework for Cypress vs Playwright."