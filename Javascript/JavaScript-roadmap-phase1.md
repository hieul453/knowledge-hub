# Learning Roadmap: JavaScript — Phase 1 (for QAOps / Test Automation + Full-Stack)
 
**Goal:** Become fluent enough in JavaScript to (1) think and program generally, (2) write real test automation — unit, API, and end-to-end — and (3) build a small full-stack app and test it end to end.
**Context:** QAOps / automation testing is the primary driver; general programming literacy and full-stack (FE/BE) capability are the supporting goals.
**Time budget:** Flexible / intensive. Full roadmap is ~80–110 hours of focused work.
**Starting point:** Total beginner — no prior programming assumed.
 
---
 
## 🗺️ Overview
You start by learning JavaScript as a *programming language* (the part that's identical whether you're testing, building frontends, or scripting servers). Once the language clicks, you branch into the browser/DOM (so automation tools make sense), then tooling and the Node runtime. From there the roadmap turns toward your real goal: unit testing, then full Playwright end-to-end + API automation, and finally a capstone where you build a small full-stack app and write a complete test suite for it.
 
---
 
## Prerequisites (Complete Before Stage 1)
- [ ] **Dev environment** — install Node.js (LTS), VS Code, and a modern browser with DevTools. You can't run a single line of JS without this. — est. 1 hr
- [ ] **Terminal basics** — `cd`, `ls`, running a command, where you are in the filesystem. Every tool you'll use is run from the terminal. — est. 1–2 hrs
- [ ] **Git basics** — you already have a Git learning plan in progress; you only need "init / add / commit / push" level here. Don't block on mastering Git internals. — est. 0–1 hr
> ✅ Skip any you already know. If unsure, skim and move on — these are gates, not subjects.
 
---
 
## Stage 1: Core Language Fundamentals — Foundation 🔴
**Goal of this stage:** Read and write basic JavaScript: store values, make decisions, repeat work, and bundle logic into functions.
**Estimated time:** 10–12 hours
**Milestone:** You're done when you can write a small script (e.g. a number-guessing game or a tip calculator) from scratch without copying, using variables, conditionals, loops, and functions.
 
### Must-Know Topics 🔴
- [ ] Variables & `let`/`const` — the difference matters and shows up in every codebase
- [ ] Data types (string, number, boolean, `null`, `undefined`) — the raw material of all programs
- [ ] Operators & type coercion — JS's coercion rules are a famous source of bugs; meet them early
- [ ] Conditionals (`if`/`else`, `switch`, ternary) — branching logic
- [ ] Loops (`for`, `while`, `for...of`) — repeating work
- [ ] Functions (declaration, parameters, return, arrow functions) — the unit of reuse
### Should-Know Topics 🟡
- [ ] `"use strict"` and modern vs. legacy mode — context for why old code looks different
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each, in order:
> 1. "Teach me JavaScript variables, data types, and type coercion. Quiz me on what coerces to what."
> 2. "Teach me control flow in JS — conditionals and loops — and verify I can trace execution by hand."
> 3. "Teach me JavaScript functions including arrow functions and return values; make sure I understand the difference."
 
---
 
## Stage 2: Data, Collections & Functional Thinking 🔴
**Goal of this stage:** Work with structured data and write expressive code using arrays, objects, and higher-order functions.
**Estimated time:** 12–15 hours
**Milestone:** You can take an array of objects (e.g. a list of test results) and filter, transform, and summarize it using `map`/`filter`/`reduce` without reaching for a `for` loop.
 
### Must-Know Topics 🔴
- [ ] Arrays and core methods (`push`, `slice`, `includes`, indexing) — the workhorse collection
- [ ] Objects, properties, and methods — how JS models "things"
- [ ] Higher-order array methods (`map`, `filter`, `reduce`, `find`, `forEach`) — these dominate real JS
- [ ] Destructuring & spread/rest — modern syntax you'll see everywhere
- [ ] Scope & closures — *the* concept that separates beginners from intermediates; critical for understanding test fixtures later
### Should-Know Topics 🟡
- [ ] `this` and how it binds — confusing but important; revisit when it bites you
- [ ] Classes & basic OOP — used in Page Object Models for test automation later
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me JS arrays and objects, then quiz me on accessing and mutating nested data."
> 2. "Teach me map, filter, and reduce with realistic examples; verify I can chain them."
> 3. "Teach me scope and closures deeply — I want to truly understand them, not just recognize them."
 
---
 
## Stage 3: Asynchronous JavaScript & the Runtime 🔴
**Goal of this stage:** Understand how JS handles things that take time — network calls, timers — without freezing, and write code that waits correctly.
**Estimated time:** 10–14 hours
**Milestone:** You can fetch data from a public API, handle success and failure, and explain in your own words why `await` doesn't block the whole program.
 
### Must-Know Topics 🔴
- [ ] The event loop & single-threaded model — *why* async exists in JS; this is the mental model everything rests on
- [ ] Callbacks → Promises → `async`/`await` — the evolution, and why `async`/`await` won
- [ ] `fetch` and working with APIs/JSON — you'll do this constantly in API testing
- [ ] Error handling (`try`/`catch`, rejected promises) — tests live or die on handling failure correctly
### Should-Know Topics 🟡
- [ ] `Promise.all` and concurrency — running things in parallel; relevant to fast test suites
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the JavaScript event loop and why JS is single-threaded but non-blocking. Verify my mental model with a trace."
> 2. "Teach me promises and async/await; quiz me on converting callback code to async/await."
> 3. "Teach me to fetch and handle data from an API including error cases; verify I handle failures."
 
---
 
## Stage 4: The Browser & the DOM 🟡
**Goal of this stage:** Manipulate web pages with JS and understand the structure that automation tools target.
**Estimated time:** 8–10 hours
**Milestone:** You can build a small interactive page (e.g. a to-do list) that responds to clicks and form input — and you understand selectors well enough that Playwright locators will feel familiar.
 
### Must-Know Topics 🔴
- [ ] DOM tree & selecting elements (`querySelector`, etc.) — Playwright locators are built on exactly this idea
- [ ] Events & event listeners — how user interaction works, which automation simulates
- [ ] Forms & input handling — the most-tested UI surface
### Should-Know Topics 🟡
- [ ] DOM manipulation (creating/removing nodes) — useful for FE, less for testing
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the DOM and element selection; verify I can target elements precisely (this maps to test locators)."
> 2. "Teach me DOM events and form handling; quiz me on what fires when."
 
---
 
## Stage 5: Tooling, Modules & the Node Runtime 🔴
**Goal of this stage:** Run JS outside the browser, manage dependencies, and split code into reusable modules — the substrate every testing framework sits on.
**Estimated time:** 6–8 hours
**Milestone:** You can `npm init` a project, install a package, write code split across ES modules, and run it with Node.
 
### Must-Know Topics 🔴
- [ ] `npm` & `package.json` — every testing tool installs this way
- [ ] ES modules (`import`/`export`) — how modern projects are organized
- [ ] Node.js basics (running files, reading args, the standard library at a glance) — the runtime your tests execute in
### Should-Know Topics 🟡
- [ ] `npx` and running CLI tools — how you'll launch Playwright/test runners
- [ ] A note on TypeScript — most Playwright projects use it; you don't need it yet, but know it exists and why teams adopt it
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me npm, package.json, and ES modules; verify I can structure a multi-file project."
> 2. "Teach me the basics of running JavaScript with Node.js outside the browser."
 
---
 
## Stage 6: Testing Fundamentals — Unit Testing 🔴
**Goal of this stage:** Write your first automated tests and understand the core testing vocabulary that applies to every level above it.
**Estimated time:** 8–10 hours
**Milestone:** You can write a test suite for a small module — arrange/act/assert, multiple cases, a mock — and run it green.
 
### Must-Know Topics 🔴
- [ ] What a test runner does & the AAA pattern (Arrange-Act-Assert) — the shape of every test you'll ever write
- [ ] Writing tests with Vitest or Jest (`describe`, `it`/`test`, `expect`) — the foundational tooling
- [ ] Assertions & matchers — how you express "what should be true"
- [ ] Mocks, stubs & test isolation — keeping tests fast and independent (your closures knowledge pays off here)
### Should-Know Topics 🟡
- [ ] Code coverage — what it tells you and what it doesn't
- [ ] Test structure & naming conventions — maintainability of a growing suite
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me unit testing fundamentals and the Arrange-Act-Assert pattern; verify I understand why isolation matters."
> 2. "Teach me to write and run tests with Vitest/Jest including assertions; quiz me on choosing matchers."
> 3. "Teach me mocking and stubbing in tests; verify I understand when and why to mock."
 
---
 
## Stage 7: End-to-End & API Test Automation with Playwright 🔴
**Goal of this stage:** Automate a real browser and a real API — the core QAOps skill set.
**Estimated time:** 12–16 hours
**Milestone:** You can write a Playwright suite that logs into a site, fills a form, asserts on the result, *and* a separate suite that tests a REST API directly — both runnable headless from the command line.
 
### Must-Know Topics 🔴
- [ ] Playwright setup & first test — `npm init playwright`, project structure
- [ ] Locators & auto-waiting — why Playwright is less flaky than older tools; ties directly to your DOM knowledge
- [ ] Web-first assertions (`expect(locator)`) — how you assert against a live page
- [ ] Actions: click, fill, navigate, wait — simulating a user
- [ ] API testing with Playwright's `request` fixture — testing endpoints without a UI
- [ ] Fixtures & test isolation (browser contexts) — clean state per test; your scope/closures + unit-testing isolation knowledge converge here
### Should-Know Topics 🟡
- [ ] Page Object Model — structuring a maintainable suite (this is where classes/OOP earn their place)
- [ ] Trace viewer & debugging flaky tests — the day-to-day reality of automation
- [ ] Reporters (HTML, JUnit) — how results feed into CI
### Nice-to-Know Topics 🟢
- [ ] Running Playwright in CI (GitHub Actions) — connects testing to the "Ops" in QAOps
- [ ] Parallelization & sharding — scaling a suite
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Playwright setup, locators, and auto-waiting; verify I understand why it reduces flakiness."
> 2. "Teach me Playwright actions and web-first assertions; quiz me on writing a login + form test."
> 3. "Teach me API testing with Playwright's request fixture; verify I can test a REST endpoint end to end."
> 4. "Teach me the Page Object Model and fixtures for maintainable Playwright suites."
 
---
 
## Stage 8: Capstone — Build a Full-Stack App & Test It 🔴
**Goal of this stage:** Tie all three goals together: build something real, then prove it works with a layered test suite.
**Estimated time:** 12–20 hours
**Milestone:** A working mini full-stack app (small Node/Express API + simple frontend) with unit tests on the backend logic, API tests on the endpoints, and Playwright E2E tests on the UI — all running with one command.
 
### Must-Know Topics 🔴
- [ ] A minimal Node/Express API — enough backend to have something to test
- [ ] A simple frontend that consumes it — closing the full-stack loop
- [ ] Layered testing strategy (the test pyramid) — what to test at each level and why
- [ ] Wiring unit + API + E2E suites together — your full QAOps toolkit applied to one project
### Should-Know Topics 🟡
- [ ] Continuous integration run of the whole suite — the "Ops" payoff
- [ ] Test data management — setup/teardown for reliable runs
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me to build a minimal Express API; verify I understand routes and request/response."
> 2. "Teach me the test pyramid; verify I can decide what belongs in unit vs API vs E2E."
> 3. "Walk me through wiring a full test suite (unit + API + E2E) for my capstone app and running it in CI."
 
---
 
## 🏁 Final Milestone
By the end, you can: read and write idiomatic modern JavaScript; explain async behavior and the event loop; build a small full-stack app; and — the main goal — author a maintainable, layered automated test suite (unit, API, and Playwright E2E) and run it in a CI pipeline. That is a working QAOps-engineer JavaScript foundation.
 
---
 
## ⏭️ What's Out of Scope (For Now)
- **Frontend frameworks (React/Vue/etc.)** — huge topic; learn after fundamentals are solid. Not needed for test automation.
- **TypeScript deep-dive** — flagged in Stage 5; worth learning *after* this roadmap, especially since most pro Playwright suites use it.
- **Performance/load testing, visual testing, mobile testing** — advanced QAOps layers; revisit once E2E is comfortable.
- **Advanced backend (databases, auth, deployment)** — the capstone stays deliberately minimal so testing stays the focus.
- **Algorithms/interview prep** — separate track; say the word and we can plan it.
---
 
## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — "Teach me JavaScript variables, data types, and type coercion. Quiz me on what coerces to what."
2. Stage 1 — "Teach me control flow in JS — conditionals and loops — and verify I can trace execution by hand."
3. Stage 1 — "Teach me JavaScript functions including arrow functions and return values; make sure I understand the difference."
4. Stage 2 — "Teach me JS arrays and objects, then quiz me on accessing and mutating nested data."
5. Stage 2 — "Teach me map, filter, and reduce with realistic examples; verify I can chain them."
6. Stage 2 — "Teach me scope and closures deeply — I want to truly understand them, not just recognize them."
7. Stage 3 — "Teach me the JavaScript event loop and why JS is single-threaded but non-blocking. Verify my mental model with a trace."
8. Stage 3 — "Teach me promises and async/await; quiz me on converting callback code to async/await."
9. Stage 3 — "Teach me to fetch and handle data from an API including error cases; verify I handle failures."
10. Stage 4 — "Teach me the DOM and element selection; verify I can target elements precisely (this maps to test locators)."
11. Stage 4 — "Teach me DOM events and form handling; quiz me on what fires when."
12. Stage 5 — "Teach me npm, package.json, and ES modules; verify I can structure a multi-file project."
13. Stage 5 — "Teach me the basics of running JavaScript with Node.js outside the browser."
14. Stage 6 — "Teach me unit testing fundamentals and the Arrange-Act-Assert pattern; verify I understand why isolation matters."
15. Stage 6 — "Teach me to write and run tests with Vitest/Jest including assertions; quiz me on choosing matchers."
16. Stage 6 — "Teach me mocking and stubbing in tests; verify I understand when and why to mock."
17. Stage 7 — "Teach me Playwright setup, locators, and auto-waiting; verify I understand why it reduces flakiness."
18. Stage 7 — "Teach me Playwright actions and web-first assertions; quiz me on writing a login + form test."
19. Stage 7 — "Teach me API testing with Playwright's request fixture; verify I can test a REST endpoint end to end."
20. Stage 7 — "Teach me the Page Object Model and fixtures for maintainable Playwright suites."
21. Stage 8 — "Teach me to build a minimal Express API; verify I understand routes and request/response."
22. Stage 8 — "Teach me the test pyramid; verify I can decide what belongs in unit vs API vs E2E."
23. Stage 8 — "Walk me through wiring a full test suite (unit + API + E2E) for my capstone app and running it in CI."