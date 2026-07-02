# Learning Roadmap: TypeScript — Phase 1

**Goal:** Become fluent enough in TypeScript to (1) add types to your test automation (Cypress/Playwright) with confidence, (2) build and type a small full-stack app, and (3) reason about types as a general programming skill — understanding *why* the type system behaves the way it does, not just sprinkling `: string` until the red squiggles disappear.
**Context:** QAOps / test automation is the primary driver; full-stack (FE/BE) capability and general programming fluency are weighted equally. TypeScript is the natural next step flagged at the end of your JavaScript Phase 1 roadmap.
**Time budget:** ~50–75 hrs of focused study + practice. No fixed schedule — estimates are in hours so you can pace yourself. Add your own reps on a real project (converting a Cypress spec, typing an Express route).
**Starting point:** JavaScript Phase 1 complete. This roadmap **assumes** you already have async/await, closures, objects/arrays, ES modules, Node/npm, unit testing, and Playwright/Express basics. If you haven't finished JS Phase 1 yet, do that first — TypeScript is a *type layer on top of JavaScript*, and every gap in your JS understanding becomes a gap in your TS understanding.

---

## 🗺️ Overview

TypeScript is JavaScript plus a **static type system that runs at compile time and disappears at runtime** — that single fact (types are erased; they never execute) explains most of what surprises beginners. So this roadmap starts there: what TS actually is, the compiler, and the mental model of "types describe the *shape* of your data." From there it builds the type system from the ground up — primitives and inference, then functions/objects/interfaces, then the deep reuse stage (generics), then the type system *at work* (narrowing and utility types), and finally lands exactly where your goals point: typing your real Cypress/Playwright suites, typing an Express API, and a capstone that ties all three goals together. By the end you won't just make errors go away — you'll know *why* the compiler complained.

---

## ⚠️ A Note On Your Starting Point (read this)

You picked "all three goals evenly," which is the right call — the core type system is identical whether you're typing a test, a React prop, or an API response. But it means **you can't skip the fundamentals to rush to "typing Cypress"**. The reason `cy.get()` autocompletes, the reason a custom command needs a `declare global` block, the reason an API response type propagates into your tests — all of it is just generics + interfaces + declaration merging applied. Learn the machine first (Stages 1–5), then point it at your tools (Stage 6). The must-knows are flagged 🔴; don't skip those.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **JavaScript Phase 1 (or equivalent)** 🔴 — variables, functions, objects/arrays, ES6, and especially **closures, `this`, async/await, and ES modules**. TS is a layer *on top* of these; you can't type what you don't understand. — est. covered by your JS roadmap
- [ ] **Node.js & npm** 🔴 — installing dev dependencies, `package.json`, running npm scripts. You install TypeScript via npm and run `tsc` on Node. — est. 0–1 hr (you have this from JS Phase 1)
- [ ] **A TS-aware editor** 🟡 — VS Code (it *is* powered by TypeScript under the hood, so the in-editor experience is the best way to learn). Know how to read an inline error and hover a variable to see its inferred type. — est. 30 min
> ✅ Skip any you already know. If unsure about JS async/closures specifically — **don't skip it.** TS makes those gaps louder, not quieter.

---

## Stage 1: What TypeScript Actually Is — The Compiler & Mental Model
**Goal of this stage:** Be able to explain, in plain language, that TypeScript is a *compile-time type checker that erases to plain JavaScript*, and get a first `.ts` file type-checking and compiling.
**Estimated time:** 4–6 hrs
**Milestone:** You can install TypeScript, run `tsc` (or use `ts-node`/the Playground), explain what `tsconfig.json` is for, and articulate "types are checked before my code runs and then thrown away — they don't exist at runtime."

### Must-Know Topics 🔴
- [ ] TS as a **superset of JS** — all valid JS is valid TS; TS adds a type layer and nothing else at runtime (this is the root fact everything else follows from)
- [ ] The compiler `tsc` — TS → JS; **type erasure** (types vanish in the emitted JS); why TS *never changes runtime behavior*
- [ ] Install & setup — `npm i -D typescript`, `npx tsc --init`, a first `hello.ts`, the TypeScript Playground for quick experiments
- [ ] `tsconfig.json` at a glance — what it is (you'll go deep in Stage 6); `strict` mode and *why you want it on from day one*
- [ ] **Type inference** — TS infers types from values; you don't annotate everything (this surprises people coming from Java/C#)

### Should-Know Topics 🟡
- [ ] `.ts` vs `.d.ts` (declaration) files — the difference at a glance (deep dive in Stage 6)
- [ ] Static vs dynamic typing — where TS sits, and the trade-off it makes

### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what TypeScript fundamentally is — a compile-time type layer that erases to JavaScript. Quiz me on *why* types don't exist at runtime and what that means in practice."
> 2. "Walk me through installing TypeScript, running `tsc`, and the role of `tsconfig.json` and `strict` mode. Make sure I understand type inference vs explicit annotation."

---

## Stage 2: The Core Type System — Primitives, Inference & Unions
**Goal of this stage:** Confidently annotate and let TS infer the everyday types, and understand the special types (`any`, `unknown`, `never`) that trip everyone up.
**Estimated time:** 8–10 hrs
**Milestone:** You can type variables, arrays, and tuples; build union and literal types; and correctly explain the difference between `any` and `unknown` and when each is (in)appropriate.

### Must-Know Topics 🔴
- [ ] Primitive types — `string`, `number`, `boolean`, `null`, `undefined`; annotation syntax vs letting inference do it
- [ ] Arrays & tuples — `string[]`, `Array<T>`, fixed-shape tuples `[number, string]`
- [ ] **Union types** (`string | number`) and **literal types** (`"GET" | "POST"`) — the backbone of expressive TS; huge for typing API methods, statuses, config
- [ ] `any` vs `unknown` vs `never` — `any` opts *out* of checking (avoid it), `unknown` is the safe unknown, `never` is the impossible type; knowing these separates beginners from intermediates
- [ ] `type` aliases — naming a type so you can reuse it

### Should-Know Topics 🟡
- [ ] Type assertions (`as`) and the non-null assertion (`!`) — the escape hatches, and why they're less safe than real types
- [ ] `enum` vs union-of-literals — what enums are, why the community often prefers plain unions
- [ ] `satisfies` — validate a value against a type *without* widening it (modern, very useful for config objects)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me TypeScript's core types — primitives, arrays, tuples, and especially union and literal types. Quiz me by giving me real data (an API response, a config) and asking me to type it."
> 2. "Teach me `any` vs `unknown` vs `never`, plus type assertions and `satisfies`. Drill me on when using `any` is a mistake and what to reach for instead."

---

## Stage 3: Shaping Data — Functions, Objects, Interfaces & Classes
**Goal of this stage:** Type the two things every program is made of — functions and object shapes — and understand structural typing, the idea that underpins all of TS.
**Estimated time:** 8–11 hrs
**Milestone:** You can fully type a function (params, optional/default/rest, return), model an object with an `interface`, explain `interface` vs `type`, and understand *why* TS uses **structural** (shape-based) typing rather than name-based.

### Must-Know Topics 🔴
- [ ] Typing functions — parameter types, return types, optional (`?`) and default params, rest params, `void`
- [ ] Object types & **interfaces** — modeling "things"; `readonly`, optional properties, index signatures (`[key: string]: T`)
- [ ] **`interface` vs `type`** — what each can/can't do, declaration merging (matters a lot for Stage 6 custom commands), when to pick which
- [ ] **Structural typing ("duck typing")** — TS cares about *shape*, not the name of the type; *the* mental model for why assignments succeed or fail
- [ ] Function types & callbacks — typing a function you pass as an argument (you'll do this constantly in test fixtures and event handlers)

### Should-Know Topics 🟡
- [ ] Classes in TS — access modifiers (`public`/`private`/`protected`), parameter properties, `implements`, abstract classes — the foundation for a typed **Page Object Model**
- [ ] Excess property checks — why an object literal errors on extra props but a variable doesn't

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me typing functions and object shapes with interfaces in TypeScript, including optional/rest params, `readonly`, and index signatures. Quiz me on modeling real data."
> 2. "Teach me structural typing and `interface` vs `type` deeply — I want to understand *why* TS accepts or rejects an assignment based on shape. Then show me how classes and access modifiers set up a typed Page Object Model."

---

## Stage 4: Generics — Reusable, Type-Safe Abstractions 🧠
**Goal of this stage:** This is the *deep understanding* stage. Internalize generics — how one piece of code stays type-safe across many types — because every advanced type you'll ever read (including `cy.get<T>()`, Playwright fixtures, `Promise<T>`, utility types) is built on them.
**Estimated time:** 8–12 hrs (slow down here — this is the payoff for "deeply")
**Milestone:** You can write a generic function and interface, use `extends` to constrain a generic, explain what `Promise<T>` and `Array<T>` really mean, and read a generic signature from a library without panic.

### Must-Know Topics 🔴
- [ ] What generics are and the problem they solve — reuse *without* losing type safety (the alternative is `any`, which throws safety away)
- [ ] Generic functions — `function identity<T>(x: T): T`; how TS **infers** the type argument from the call
- [ ] Generic interfaces & types — `interface Box<T>`, and reading built-ins like `Promise<T>`, `Array<T>`, `Record<K, V>`
- [ ] **Generic constraints** — `<T extends { id: number }>`; limiting what a generic accepts
- [ ] Why generics matter for *you* — this is literally how Cypress's `Chainable<T>` and Playwright's fixtures are typed; reusable test helpers need them

### Should-Know Topics 🟡
- [ ] Default generic parameters (`<T = string>`)
- [ ] Multiple type parameters and how they relate (`<K, V>`)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me generics in TypeScript from the ground up — the problem they solve, generic functions, and type-argument inference. Quiz me hard: give me `any`-typed code and make me generic it correctly."
> 2. "Teach me generic interfaces and constraints (`extends`), and walk me through reading real generic signatures like `Promise<T>`, `Array<T>`, and Cypress's `Chainable<T>`. Verify I can explain each."

---

## Stage 5: The Type System at Work — Narrowing, Guards & Utility Types
**Goal of this stage:** Use the type system the way real code does — narrowing a union down to a specific type safely, and reshaping existing types instead of rewriting them.
**Estimated time:** 8–12 hrs
**Milestone:** You can narrow a `string | undefined` safely, write a type guard and a discriminated union, and reach for the right utility type (`Partial`, `Pick`, `Omit`, `Record`, `Awaited`) instead of hand-writing a new type.

### Must-Know Topics 🔴
- [ ] **Narrowing & control-flow analysis** — how `typeof`, `in`, truthiness, and `===` checks narrow a type inside an `if`; *why* TS knows the type is safe after the check
- [ ] **Type guards** — user-defined `x is Foo` predicates; narrowing custom types
- [ ] **Discriminated unions** — a shared literal "tag" field that lets TS pick the right variant; the cleanest way to model states (loading/success/error), events, API results
- [ ] **Utility types** — `Partial`, `Required`, `Readonly`, `Pick`, `Omit`, `Record`, `Awaited`; deriving types from types instead of duplicating them
- [ ] Handling `null`/`undefined` under `strictNullChecks` — optional chaining, narrowing, and why strict null checking prevents a whole bug class

### Should-Know Topics 🟡
- [ ] `keyof` and indexed access types (`T["field"]`) — the building blocks under the utility types
- [ ] Assertion functions (`asserts x is Foo`) — narrowing via a thrown-error helper (handy in test setup/validation)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me type narrowing and control-flow analysis in TypeScript — `typeof`, `in`, truthiness, type guards, and discriminated unions. Give me unions and make me narrow them safely; quiz me on why each narrows."
> 2. "Teach me the built-in utility types (`Partial`, `Pick`, `Omit`, `Record`, `Awaited`) plus `keyof`. Give me a base type and make me derive new ones without rewriting anything."

---

## Stage 6: TypeScript in Your Real Tools — Config, `@types`, Node/Express & Cypress
**Goal of this stage:** Point everything you've learned at your actual stack: configure a real project, type an Express API, and write a fully typed Cypress (and Playwright) suite — the QAOps + full-stack payoff.
**Estimated time:** 8–12 hrs
**Milestone:** You can configure a `tsconfig.json` deliberately, install and use `@types/*` packages, type an Express route (`Request`/`Response`), and set up Cypress with TypeScript including a typed custom command via `declare global` / declaration merging.

### Must-Know Topics 🔴
- [ ] `tsconfig.json` in depth — `target`, `lib`, `module`, `moduleResolution`, `strict`, `types`, `include`/`exclude`; the options that actually matter
- [ ] **Declaration files & `@types`** — what `.d.ts` files are, `DefinitelyTyped`/`@types/node`, `@types/express`; how types get attached to plain-JS libraries
- [ ] **Typing your tests** — Cypress ships its own types; TS 5.x/6.x required; the `cypress/tsconfig.json` with `"types": ["cypress", "node"]`; typing a **custom command** via `declare global { namespace Cypress { interface Chainable {...} } }` (this is Stage 3's declaration merging + Stage 4's generics in the wild)
- [ ] **Typing an Express API** — typed `Request`/`Response`, typed route handlers, sharing a response-shape type between the API and the tests that hit it
- [ ] Running typed tests in CI — `tsc --noEmit` as a type-check step in your GitHub Actions pipeline (ties into your Git roadmap's CI stage)

### Should-Know Topics 🟡
- [ ] Playwright is **TypeScript-native** — `npm init playwright` scaffolds TS by default; contrast with Cypress's opt-in setup
- [ ] `ts-node` / on-the-fly compilation, and how Cypress compiles specs for you
- [ ] Sharing types across front end + back end + tests — the full-stack "one source of truth" win

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `tsconfig.json` in depth and how declaration files and `@types` packages work. Quiz me on which compiler options matter and why `@types/node` exists."
> 2. "Teach me setting up Cypress with TypeScript and typing a custom command with declaration merging, then typing an Express route. Connect it back to generics and interfaces, and to running `tsc --noEmit` in CI."

---

## Stage 7: Capstone — Type a Full-Stack App & Its Test Suite
**Goal of this stage:** Tie all three goals together in one project: convert (or build) a small full-stack app to TypeScript, share types across the stack, and prove it works with a typed test suite.
**Estimated time:** 8–14 hrs
**Milestone:** A small full-stack app (typed Node/Express API + simple frontend) with a **shared types module**, plus a typed test suite (unit + API + Cypress/Playwright E2E) — where a change to a response type surfaces as compile errors in every test that's now wrong, all running in CI with a `tsc --noEmit` gate.

### Must-Know Topics 🔴
- [ ] Convert a small JS app to TS (or build minimal from scratch) — `tsconfig`, incremental typing, killing `any`s
- [ ] A **shared types module** — one `types.ts` imported by the API, the frontend, and the tests (the payoff of the full-stack + QAOps combination)
- [ ] A typed layered test suite — unit tests, API tests, and Cypress/Playwright E2E, all in TS, all sharing the app's types
- [ ] The refactor test — change a type on purpose and watch the compiler point at every broken test *before* you run anything

### Should-Know Topics 🟡
- [ ] CI run of the whole suite with a type-check step — the "Ops" payoff
- [ ] Where to turn strictness up next (`noUncheckedIndexedAccess`, etc.) once the app is green

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Walk me through converting a small Express + frontend app to TypeScript with a shared types module. Verify I understand how one type change propagates across the stack."
> 2. "Walk me through wiring a fully typed test suite (unit + API + E2E) that shares the app's types, and gating it in CI with `tsc --noEmit`. Quiz me on what the shared types buy me."

---

## 🏁 Final Milestone
You can take a JavaScript codebase — including your existing Cypress/Playwright suites — and add TypeScript to it deliberately: configure the compiler, model your data with interfaces and unions, write generic reusable helpers, narrow types safely, type your Express routes and custom commands, share one source of type truth across app + tests, and gate it all in CI. And — the "deeply" part — you can explain to another engineer *why* the compiler accepts or rejects a given piece of code (type erasure, structural typing, inference, narrowing), not just recite annotation syntax.

---

## ⏭️ What's Out of Scope (For Now)

- **Advanced type-level programming** — conditional types, mapped types, template literal types, recursive types. Fascinating and powerful, but a Phase 2 topic; you only need to *read* them, not author them, to be productive.
- **TypeScript with React/Vue** (typed props, hooks, generics in components) — a strong "next" once the core model is solid, especially for the frontend half of full-stack. Separate roadmap.
- **Decorators & metadata** (heavily used in NestJS/Angular) — situational; learn the day a framework forces it on you.
- **Writing & publishing your own `.d.ts` for a JS library / contributing to DefinitelyTyped** — advanced; revisit after you're comfortable *consuming* types.
- **Monorepo TS setup, project references, build performance tuning** — real-team concerns, but not needed to learn the language.
- **`tsc` internals / the compiler API** — deep mastery territory; not on the path to your goal.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — What TS is: "Teach me what TypeScript fundamentally is — a compile-time type layer that erases to JavaScript. Quiz me on why types don't exist at runtime and what that means in practice."
2. Stage 1 — Setup: "Walk me through installing TypeScript, running `tsc`, and the role of `tsconfig.json` and `strict` mode. Make sure I understand type inference vs explicit annotation."
3. Stage 2 — Core types: "Teach me TypeScript's core types — primitives, arrays, tuples, and especially union and literal types. Quiz me by giving me real data and asking me to type it."
4. Stage 2 — any/unknown/never: "Teach me `any` vs `unknown` vs `never`, plus type assertions and `satisfies`. Drill me on when `any` is a mistake and what to use instead."
5. Stage 3 — Functions & interfaces: "Teach me typing functions and object shapes with interfaces, including optional/rest params, `readonly`, and index signatures. Quiz me on modeling real data."
6. Stage 3 — Structural typing: "Teach me structural typing and `interface` vs `type` deeply — why TS accepts or rejects assignments by shape. Then show me how classes set up a typed Page Object Model."
7. Stage 4 — Generics: "Teach me generics from the ground up — the problem they solve, generic functions, and type-argument inference. Quiz me hard: make me generic-ify `any`-typed code."
8. Stage 4 — Generic constraints: "Teach me generic interfaces and constraints (`extends`), and reading real signatures like `Promise<T>` and Cypress's `Chainable<T>`. Verify I can explain each."
9. Stage 5 — Narrowing: "Teach me type narrowing and control-flow analysis — `typeof`, `in`, truthiness, type guards, discriminated unions. Make me narrow unions safely; quiz me on why each narrows."
10. Stage 5 — Utility types: "Teach me the built-in utility types (`Partial`, `Pick`, `Omit`, `Record`, `Awaited`) plus `keyof`. Give me a base type and make me derive new ones."
11. Stage 6 — Config & @types: "Teach me `tsconfig.json` in depth and how declaration files and `@types` packages work. Quiz me on which compiler options matter and why `@types/node` exists."
12. Stage 6 — Typing tests & Express: "Teach me setting up Cypress with TypeScript and typing a custom command with declaration merging, then typing an Express route. Connect it to generics and to `tsc --noEmit` in CI."
13. Stage 7 — Capstone convert: "Walk me through converting a small Express + frontend app to TypeScript with a shared types module. Verify I understand how one type change propagates across the stack."
14. Stage 7 — Capstone tests + CI: "Walk me through wiring a fully typed test suite (unit + API + E2E) that shares the app's types, gated in CI with `tsc --noEmit`. Quiz me on what shared types buy me."
