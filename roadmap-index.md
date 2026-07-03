# Roadmap Index (Quick-Check Reference)

Update this file whenever a roadmap is added or extended. Purpose: fast overlap check before generating a new roadmap — open the actual file for detail.

## Git — Phase 1 (Team Collaboration)
Stages: 1 Mental model & setup (snapshot data model, 3 areas, init/clone) · 2 Daily loop (status/add/commit/diff/log, .gitignore) · 3 Branching & merging (branches, merge, conflicts, rebase basics) · 4 Undo & recovery (restore, amend, reset, revert, reflog, stash) · 5 Remotes & collaboration (remote, fetch/pull/push, basic PR workflow, GitHub flow) · 6 Pro/QAOps workflows (branching strategies, tags, CI triggers from Git events, bisect, hooks)
Out of scope: plumbing internals, history rewriting/filter-repo, submodules, GUI clients.

## GitHub — Phase 1 (The Platform)
Explicitly excludes Git engine mechanics (owned by the Git roadmap) — covers the platform layered on top.
Stages: 1 Platform & repos (repo creation/visibility, repo UI, GFM markdown, SSH/PAT auth, gh CLI) · 2 Collaboration surfaces (Issues/templates, issue↔PR linking, PR *review* UI, Discussions, CODEOWNERS) · 3 Planning (Projects table/board/roadmap, custom fields/iterations, milestones/labels, automations) · 4 Actions I (events/workflows/jobs/steps model, runners, YAML anatomy, first CI workflow as PR check) · 5 Actions II (secrets, GITHUB_TOKEN/permissions, caching, matrix builds, artifacts, wiring a real E2E suite into CI) · 6 Governance/security/releases (branch protection/rulesets, permission levels, Dependabot/secret scanning/CodeQL, releases/tags)
Out of scope: Git internals, org/enterprise admin, custom Actions authoring, REST/GraphQL/webhooks/Apps, Codespaces, Copilot, full CD.

## JavaScript — Phase 1 (QAOps + Full-Stack)
Stages: 1 Core fundamentals (vars, types, coercion, conditionals, loops, functions) · 2 Data/collections/functional (arrays, objects, map/filter/reduce, destructuring/spread, closures, `this`, classes) · 3 Async & runtime (event loop, callbacks→promises→async/await, fetch, error handling) · 4 Browser & DOM (DOM tree/selectors, events, forms) · 5 Tooling/modules/Node (npm, package.json, ES modules, Node basics) · 6 Unit testing fundamentals (test runner, AAA, Vitest/Jest, mocks/stubs, coverage) · 7 Playwright E2E + API automation (setup, locators/auto-wait, web-first assertions, actions, API testing, fixtures, POM, CI/parallelization intro) · 8 Capstone (Express API + frontend + layered suite + CI)
Out of scope: frontend frameworks, TS deep-dive (→ separate TS roadmap), perf/load/visual/mobile testing, advanced backend, algorithms.

## TypeScript — Phase 1
Assumes JS Phase 1 complete.
Stages: 1 Compiler & mental model (superset of JS, type erasure, tsc, tsconfig, strict, inference) · 2 Core type system (primitives, arrays/tuples, unions/literals, any/unknown/never, satisfies) · 3 Shaping data (function typing, interfaces, interface vs type, structural typing, classes/access modifiers) · 4 Generics (generic functions/interfaces, inference, constraints, Promise<T>/Chainable<T>) · 5 Narrowing & utility types (type guards, discriminated unions, Partial/Pick/Omit/Record/Awaited, strictNullChecks) · 6 Real tools (tsconfig depth, @types/.d.ts, **typing Cypress custom commands via declare global**, typing Express, tsc --noEmit in CI) · 7 Capstone (convert app to TS, shared types module, typed layered suite, CI type-check gate)
Out of scope: conditional/mapped/template-literal types, TS+React, decorators, monorepo/project refs, compiler internals.
⚠️ Cross-reference: Stage 6 covers TS+Cypress custom commands, which the Cypress roadmap lists as out-of-scope for itself — point back here instead of re-teaching it in a future Cypress phase.

## React (core concepts) — Phase 1
Prep track for React Native (Visual Life Archive app). Assumes JS Stages 1–3 + ES6.
Stages: 1 What React is & JSX (declarative UI, components, JSX, Vite scratch project) · 2 Components & props (props/one-way flow, composition, list rendering + key, conditional rendering) · 3 State & interactivity (useState, render loop, events, controlled inputs, state-as-snapshot) · 4 Side effects & data (useEffect + deps, fetching, loading/error/success states, cleanup) · 5 Thinking in React (one-way data flow, lifting state up, component-tree decomposition, useRef/useContext intro)
Out of scope: React Native itself (own roadmap), routing/Next.js/Server Components, state-mgmt libraries, perf hooks, TS+React, custom hooks/useReducer.
Note: styling/layout not covered here — see the Flexbox roadmap for the layout layer the React/RN frontend relies on.

## Flexbox (Layout & Styling) — Phase 1
Companion to the React / React Native frontend (Visual Life Archive app); taught universally (web CSS + React Native). Can be started in a browser before React — only Stage 4 leans on React. Prereqs: basic HTML/CSS (for the sandbox), React (for Stage 4 only).
Stages: 1 Mental model (flex container vs items, main vs cross axis, flex-direction, RN column-default preview) · 2 Aligning/distributing (justify-content, align-items, align-self, perfect centering) · 3 Sizing/flexibility (flex-grow/shrink/basis, flex shorthand + flex:1, flex-wrap, gap, align-content) · 4 Real layouts & React Native differences (header/content/footer column, wrapping card gallery, RN camelCase style objects/unitless dimensions/flexbox-only layout, aspect-ratio)
Out of scope: CSS Grid (separate topic; absent in React Native), rest of CSS (box model/positioning/animations/media queries), NativeWind/Tailwind/styled-components, responsive web beyond wrapping, RN styling beyond layout (theming/Dimensions/safe areas).

## Cypress — Phase 1
Prereqs: JS async/DOM/HTTP/Node/testing-concepts fundamentals.
Stages: 1 Architecture & first test (in-browser model vs Selenium, install, open vs run mode, describe/it/visit/get) · 2 Core commands (get/contains, data-cy selectors, interactions, assertions/Chai) · 3 Async model & retry-ability [deep] (command queue, not-Promises, retry rules, aliases vs variables, .then()) · 4 Network & test data (cy.intercept spy/stub, fixtures, cy.request, cy.session) · 5 Structuring a real suite (custom commands, test isolation, Page Object vs App Actions, component testing intro) · 6 QAOps: CI/parallelization/limits (headless run, GitHub Action, parallelization, Cypress's limits vs Playwright)
Out of scope: TS+Cypress (**now partly covered — see TypeScript Stage 6**), visual regression/a11y, BDD/Cucumber, plugin authoring, Playwright itself.

---

**Shared prerequisite recall (expected, not wasted duplication):** async/promises, npm/Node basics, DOM/selectors, and CI fundamentals appear as brief prerequisite context across Git, JS, TS, Cypress, React, and GitHub. That's intentional light overlap for grounding, not a repeated stage.