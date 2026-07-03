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

## Cypress — Phase 1
Prereqs: JS async/DOM/HTTP/Node/testing-concepts fundamentals.
Stages: 1 Architecture & first test (in-browser model vs Selenium, install, open vs run mode, describe/it/visit/get) · 2 Core commands (get/contains, data-cy selectors, interactions, assertions/Chai) · 3 Async model & retry-ability [deep] (command queue, not-Promises, retry rules, aliases vs variables, .then()) · 4 Network & test data (cy.intercept spy/stub, fixtures, cy.request, cy.session) · 5 Structuring a real suite (custom commands, test isolation, Page Object vs App Actions, component testing intro) · 6 QAOps: CI/parallelization/limits (headless run, GitHub Action, parallelization, Cypress's limits vs Playwright)
Out of scope: TS+Cypress (**now partly covered — see TypeScript Stage 6**), visual regression/a11y, BDD/Cucumber, plugin authoring, Playwright itself.
⚠️ Cross-reference: the "HTTP basics" prerequisite above is listed but never actually taught here — now covered by **REST API / HTTP Phase 1, Stage 1**. Point back there instead of teaching it in a future Cypress phase.

## SQL & Relational Databases — Phase 1
Three drivers weighted evenly: app backend (Supabase/Postgres), QAOps (test-data setup/teardown + DB state verification), general fluency. Teaches the relational engine itself; Supabase-the-platform is a separate roadmap.
Stages: 1 Relational model & setup · 2 Querying a single table (SELECT, filtering, sorting) · 3 Designing tables (data types, constraints, schema design) · 4 Relationships & JOINs · 5 Aggregation, grouping & subqueries · 6 Writing data & transactions (integrity) · 7 PostgreSQL in your real stack (Supabase, indexes, test data)
Out of scope: RLS in depth (**now covered — see Supabase Phase 1, Stage 3**), query performance tuning (EXPLAIN ANALYZE, index types), window functions/advanced analytics, stored procedures/functions/triggers (PL/pgSQL), migrations tooling deep-dive, ORMs/query builders, database administration at scale, NoSQL comparison depth.

## Supabase — Phase 1
Full-platform roadmap (schema+RLS, auth, storage, Realtime, Edge Functions, CLI/migrations/local dev) — three drivers weighted evenly: app backend, general BaaS fluency, QAOps.
Stages: 1 Platform mental model & setup · 2 Database layer — tables, relationships & auto-generated API · 3 Row Level Security & the auth-to-data security model · 4 Authentication in depth · 5 Storage — files, buckets & access policies · 6 Realtime & Edge Functions · 7 Local dev, CLI, migrations & environments · 8 QAOps — testing against Supabase, seeding & verifying state
Out of scope: deep Postgres/SQL engine (owned by SQL Phase 1), advanced RLS at scale (multi-tenant RBAC, perf tuning), self-hosting Supabase, pgvector/AI embeddings, advanced Postgres extensions (PostGIS, pg_cron, pg_net), production ops at scale, framework-specific SSR auth deep-dives, Management API/CI-CD for the platform itself.
⚠️ Cross-reference: fulfills the "RLS in depth" deferral that SQL Phase 1 explicitly pointed here — supersedes that out-of-scope note (Stage 3). Also supersedes React Native + Expo Phase 1's Supabase intro on depth: RN Stages 5–6 apply Supabase from the mobile client only; this roadmap is the deeper platform source and covers Realtime & Edge Functions, which the RN roadmap lists as out of scope.

## Auth & Secrets — Phase 1
Cross-cutting "Group 4" concept roadmap, learned alongside backend/Supabase work rather than in isolation. Not implementing auth from scratch — Supabase handles that; this builds the mental model to use it correctly and safely.
Stages: 1 Authentication fundamentals — the mental model · 2 Sessions vs tokens (and JWTs) · 3 Auth in your app — Supabase Auth on Expo · 4 Environment variables & secrets
Out of scope: building your own auth server/password hashing internals, writing RLS policies in depth/RBAC (→ Supabase Phase 1), OAuth/social-login deep flow + deep-linking, cryptography internals, CI/deployment secrets mechanics (→ GitHub Phase 1, Stage 5), secret-management platforms/key rotation, web cookie-security deep-dive.

## REST API / HTTP — Phase 1 (Consuming, Designing & Testing)
Conceptual spine (HTTP + REST theory + API-consumer concerns + tooling) that JS, React, Cypress, and Supabase roadmaps assumed but never taught directly. Concept-first, with tool mechanics referenced out to the roadmap that owns them.
Stages: 1 HTTP — the protocol (verbs/safe-idempotent-cacheable, status code families, headers, URLs/query params) · 2 REST — the architectural style (resources/representations, CRUD↔verb mapping, statelessness, Richardson Maturity Model, REST vs GraphQL/RPC) · 3 Consuming APIs in practice (auth schemes — API keys/Bearer/JWT/OAuth, CORS, pagination/filtering, error handling & resilience, exploration tooling/OpenAPI) · 4 Designing a REST API (resource modeling, URL/verb/status conventions, request/response body design, consistent errors, versioning) · 5 Testing REST APIs (three assertion layers, positive/negative/auth/boundary cases, test data & isolation, contract testing concept)
Out of scope: fetch/async/await mechanics (owned by JS Phase 1, Stage 3), data-fetching UI states (owned by React Phase 1, Stage 4), implementing a server + Supabase/PostgREST specifics + RLS (owned by JS Phase 1 Stage 8 / Supabase Phase 1), tool-specific test syntax (JS Phase 1 Stage 7 / Cypress Phase 1 Stage 4), GraphQL in depth, real-time/streaming (WebSockets/SSE/Supabase Realtime), API gateways/rate-limit implementation/CDNs/production ops, performance/load testing, gRPC/Protocol Buffers.
⚠️ Cross-reference: becomes the canonical owner of HTTP & REST fundamentals, which Cypress Phase 1 lists as a prerequisite but never actually teaches — supersedes that prerequisite bullet (see Cypress entry above).

## Flexbox — Phase 1
Universal layout roadmap — designed to serve both React Native (its actual layout system) and web CSS, with Stage 4 isolating RN-specific differences. Avoids re-teaching layout inside the React Native roadmap.
Stages: 1 Mental model — container, items & the two axes · 2 Distributing & aligning (justify-content, align-items, align-self) · 3 Sizing & flexibility (grow, shrink, basis, wrapping) · 4 Real layouts & React Native differences
Out of scope: CSS Grid (doesn't exist in RN — separate web-only roadmap later), rest of CSS (box model depth, positioning, transitions/animations, media/container queries), NativeWind/Tailwind/styled-components abstractions, responsive web design beyond wrapping, RN styling beyond layout (theming, platform-specific styles, Dimensions, safe areas).

## React Native + Expo — Phase 1
Capstone: builds the Visual Life Archive app (auth + photo storage + data, all on Supabase). Assumes React core concepts (Phase 1) + Flexbox Stage 4 as prerequisite context; JavaScript-first per established pattern — not RN mastery, the exact stack this app needs.
Stages: 1 What RN + Expo are — mental model & first screen · 2 Building UIs — core components, styling & Flexbox · 3 Lists & navigation (FlatList + Expo Router) · 4 Native capabilities — permissions, camera & photos · 5 The backend — Supabase auth, database & storage · 6 Assembling the app — auth-gated navigation & the full loop
Out of scope: TypeScript with RN (→ TypeScript Phase 1, after app + concepts are solid), shipping to app stores (→ EAS Build & Submit Phase 1), testing the RN app (Detox/Maestro/RNTL — candidate QAOps Phase 2, connects to JS/Cypress tracks), animations & gestures (Reanimated/Gesture Handler), push notifications/deep linking/social-OAuth login, Realtime & offline sync (**deeper coverage — see Supabase Phase 1, Stage 6**), state-management libraries (Redux/Zustand/TanStack Query), bare/native workflow/custom native modules/web target, React Navigation (using Expo Router instead).
⚠️ Cross-reference: its Supabase intro (Stages 5–6) is superseded on depth by Supabase Phase 1, which is the canonical source for Realtime & Edge Functions (listed out of scope here) and full Auth/Storage/RLS treatment.

## EAS Build & Submit — Phase 1
Deployment stage — takes the finished RN app from source to installable build and app-store submission via Expo's cloud build/submit (EAS); no Mac required.
Stages: 1 EAS & the build/submit mental model · 2 App identity, credentials & signing · 3 Running EAS Build · 4 Store submission & review
Out of scope: building the app/RN feature code (→ React Native + Expo Phase 1), web deployment (→ Vercel Phase 1), deep CI/CD pipeline authoring (→ GitHub Phase 1, Stage 5), manual native credential management/Fastlane, custom native modules/bare-workflow prebuild, App Store Optimization/marketing/monetization/in-app purchases, EU DMA/alternative app stores/enterprise MDM distribution.

## Vercel — Phase 1
Web-deployment counterpart to EAS (which ships the mobile apps) — deploys the Expo project's web build to a live public URL.
Stages: 1 What Vercel is & the deployment mental model · 2 Deploying the app's web version · 3 Environment variables, domains & configuration · 4 The deployment workflow & operations
Out of scope: building the web app itself (output comes from React Native + Expo Phase 1), Vercel Functions/Edge Functions/API routes (backend is Supabase, not Vercel), Next.js-specific features (SSR/ISR/App Router — app isn't Next.js), mobile app deployment (→ EAS Build & Submit Phase 1), CI test pipelines (→ GitHub Phase 1, Stage 5), DNS deep-dive/advanced CDN tuning/monorepo config/Enterprise features.

---

**Shared prerequisite recall (expected, not wasted duplication):** async/promises, npm/Node basics, DOM/selectors, and CI fundamentals appear as brief prerequisite context across Git, JS, TS, Cypress, React, and GitHub. That's intentional light overlap for grounding, not a repeated stage.