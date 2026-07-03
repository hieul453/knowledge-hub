# Learning Roadmap: REST / APIs & Data Fetching — Phase 1

**Goal:** Genuinely *understand* HTTP and REST as concepts — not just call `fetch` and hope — so you can confidently **consume** any web API in code, **design** a sane REST API, and **test** one as a QA engineer. Success = you can look at an unfamiliar API, reason about its verbs/status codes/auth/pagination from first principles, wire it into a client, and write meaningful tests against it.
**Context:** Three drivers weighted evenly — (1) **consuming** APIs for the Visual Life Archive app (you already talk to Supabase's REST/PostgREST API), (2) **designing** REST endpoints (full-stack fluency), and (3) **API testing** (your QAOps direction). This roadmap is the *conceptual spine* — HTTP + REST theory + API-consumer concerns + tooling — that your other roadmaps quietly assumed but never taught.
**Time budget:** ~32–45 hrs of focused study + practice, total. No fixed weekly schedule — estimates are in hours so you can pace yourself. APIs reward exploration: keep a real public API (or your own Supabase project) open and poke at it as you go.
**Starting point:** You've done (or are doing) JavaScript Phase 1. You can write functions, work with objects/arrays, and — critically — call `fetch`, `await` a response, parse JSON, and handle errors with `try/catch` (**JS Phase 1, Stage 3**). This roadmap builds the *why* on top of those mechanics.

---

## 🗺️ Overview

This roadmap moves from the wire up to the design table. It starts with **HTTP itself** — the protocol every web API speaks — because methods, status codes, and headers are the vocabulary the rest of the journey is built on. Then it isolates **REST** as an *architectural style* (resources, statelessness, verb↔CRUD mapping) so "RESTful" stops being a buzzword. From there it turns practical: **consuming** real APIs (auth schemes, CORS, pagination, error semantics, and exploration tooling like curl/Postman/OpenAPI), then **designing** a clean REST API (resource modeling, URL/verb/status choices, versioning, error shape), and finally **testing** REST APIs the way a QA engineer does (status/body assertions, contract testing, negative and auth cases). By the end, Supabase's auto-generated API, a hand-rolled Express API, and any third-party API you meet all read as instances of the same handful of ideas.

---

## ⚠️ A Note On How This Roadmap Is Scoped (read this)

You already have roadmaps that touch data fetching from specific angles. To avoid re-teaching, this one is deliberately **concept-first with mechanics referenced out**, decided per-topic with you:

- The raw **`fetch` mechanics** (await, parse JSON, `try/catch`) live in **JS Phase 1 Stage 3** — this roadmap adds the *why* on top and does light recall only, not re-teaching.
- **Data-fetching UI states** (loading/error/success in a component) live in **React Phase 1 Stage 4** — referenced by pointer, not a stage here.
- **Supabase's PostgREST auto-API, keys, and RLS** live in **Supabase Phase 1 Stages 1–3** — used here as the concrete "real REST API you consume" example, not re-taught.
- **Tool-specific API testing** (Playwright `request` fixture, Cypress `cy.request`/`cy.intercept`) lives in **JS Phase 1 Stage 7** and **Cypress Phase 1 Stage 4** — this roadmap teaches the *concept* of API testing tool-agnostically and points to those for the tool mechanics.
- **Building the API in Express** lives in **JS Phase 1 Stage 8** — referenced for implementation; the *design thinking* is taught here.

So when a stage says "now go apply this in JS S3 / React S4 / Cypress S4," that's intentional — you're not skipping content, you're using the roadmap that owns it.

> 📇 **Index note:** This roadmap becomes the canonical owner of **HTTP & REST fundamentals**, which the **Cypress Phase 1** prerequisites list ("HTTP basics — methods, status codes, JSON") but never actually teach. Flag this as a supersede cross-reference when you update `roadmap-index.md`.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **JavaScript async & `fetch`** 🔴 — `async`/`await`, Promises, calling `fetch`, parsing JSON, and `try/catch` error handling. This is the hands-on substrate for every "now go call a real API" exercise below. — see **JS Phase 1, Stage 3** — est. **0 hrs if already done**
- [ ] **Basic JSON literacy** 🔴 — objects, arrays, nesting, data types. You'll read and assert on JSON constantly. — covered incidentally in JS Phase 1 Stages 1–2 — est. **0–1 hr recall**
> ✅ If JS Stage 3 isn't done yet, do it first — the mechanics won't be re-taught here.

---

## Stage 1: HTTP — The Protocol Every API Speaks 🔴
**Goal of this stage:** Understand HTTP as a request/response protocol well enough that methods, status codes, and headers become a language you *read fluently* rather than memorized trivia.
**Estimated time:** 6–8 hours
**Milestone:** Given a raw HTTP request/response (from browser DevTools or `curl -v`), you can explain every part — method, path, headers, status line, body — and predict what a given method + status code combination means without looking it up.

### Must-Know Topics 🔴
- [ ] **The request/response model & client-server statelessness** — what actually travels over the wire, and why HTTP "forgets" you between requests (the fact that makes tokens/cookies necessary later).
- [ ] **HTTP methods (verbs)** — `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, `OPTIONS` — and the properties that matter: **safe**, **idempotent**, **cacheable**. Why `PUT` is idempotent but `POST` isn't is a load-bearing idea.
- [ ] **Status code families** — 1xx/2xx/3xx/4xx/5xx as *classes*, plus the everyday specifics (200, 201, 204, 301/302, 400, 401, 403, 404, 409, 422, 429, 500, 502, 503). Client-error vs server-error is the fault-line you'll debug on daily.
- [ ] **Headers** — request vs response headers; the ones you'll actually touch: `Content-Type`, `Accept`, `Authorization`, `Cache-Control`, `Location`, `Set-Cookie`. Metadata is where a lot of API behavior hides.
- [ ] **URLs, path vs query parameters, and JSON as the body format** — how a URL encodes *which resource* (path) and *how to shape the response* (query: filter/sort/paginate).

### Should-Know Topics 🟡
- [ ] **HTTP versions at a glance** — 1.1 vs 2 vs 3: same semantics, different transport. Awareness, not depth.
- [ ] **HTTPS / TLS in one paragraph** — why "always HTTPS" matters before you ever send a token.

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the HTTP request/response model and why HTTP is stateless — walk me through a real request line by line (method, path, headers, body, status). Quiz me on why statelessness forces us to send auth on every request."
> 2. "Teach me HTTP methods and the safe / idempotent / cacheable properties. Quiz me hard: give me scenarios and make me pick the right verb and justify idempotency."
> 3. "Teach me HTTP status code families and the common specific codes. Drill me with response scenarios and make me distinguish 400 vs 401 vs 403 vs 404 vs 422, and 500 vs 502 vs 503."

---

## Stage 2: REST — The Architectural Style 🔴
**Goal of this stage:** Turn "RESTful" from a buzzword into a precise set of constraints, so you can judge whether an API *is* REST-shaped and why that matters.
**Estimated time:** 5–7 hours
**Milestone:** You can explain REST's core constraints in your own words, map CRUD operations onto HTTP verbs + resource URLs, place a given API on the Richardson Maturity Model, and articulate when REST is *not* the right choice (vs GraphQL/RPC).

### Must-Know Topics 🔴
- [ ] **Resources & representations** — the central REST idea: everything is a *noun* (resource) addressed by a URL; JSON is one *representation* of it. Endpoints are nouns, not verbs (`/users/42`, not `/getUser?id=42`).
- [ ] **CRUD ↔ HTTP verb mapping** — Create/POST, Read/GET, Update/PUT|PATCH, Delete/DELETE, and collection vs item URLs (`/entries` vs `/entries/7`).
- [ ] **Statelessness as a REST constraint** — each request carries everything the server needs; why this enables scaling and shapes auth.
- [ ] **The Richardson Maturity Model** — levels 0→3 (single endpoint → resources → verbs+status codes → hypermedia/HATEOAS); most real APIs sit at level 2, and knowing that is enough to reason about them.
- [ ] **REST vs GraphQL vs RPC (awareness)** — what each optimizes for, so "why is Supabase REST but this other thing GraphQL?" has an answer.

### Should-Know Topics 🟡
- [ ] **HATEOAS / hypermedia (level 3)** — what it is, why most APIs skip it, and why you rarely need to implement it. Awareness only.
- [ ] **Where REST's constraints came from** — Fielding's dissertation in one sentence each (client-server, stateless, cacheable, uniform interface, layered). Context that makes the docs make sense.

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me REST as an architectural style — resources, representations, statelessness, and the uniform interface — and why endpoints should be nouns. Make me redesign a verb-based API (`/getUser`, `/createUser`) into a resource-based one and defend it."
> 2. "Teach me the CRUD-to-HTTP-verb mapping with collection vs item URLs, and the Richardson Maturity Model. Give me several real API endpoints and make me place each on the RMM and justify it."
> 3. "Teach me REST vs GraphQL vs RPC at a decision-making level — what each is good and bad at. Quiz me on which I'd pick for given scenarios, including my Supabase-backed app."

---

## Stage 3: Consuming APIs In Practice 🔴
**Goal of this stage:** Go from "I can call one happy-path endpoint" to "I can consume a real, authenticated, paginated third-party API and handle everything that can go wrong."
**Estimated time:** 8–11 hours
**Milestone:** You can read an unfamiliar API's docs, authenticate to it, page through a large result set, handle its error responses and rate limits gracefully, debug a CORS failure, and explore it in curl/Postman before writing a line of app code.
**Milestone (applied):** You wire one real authenticated API end-to-end using `fetch` — reusing the mechanics from JS Stage 3, not re-learning them.

### Must-Know Topics 🔴
- [ ] **API authentication schemes** — API keys (header vs query), **Bearer tokens / JWT** (`Authorization: Bearer …`), session cookies, and OAuth 2.0 at a *conceptual* level (why the redirect dance exists). This is the general pattern behind Supabase's anon/JWT keys.
- [ ] **Request/response shaping in practice** — setting `Content-Type`/`Accept`, sending a JSON body on POST/PUT, reading status + body together (a 200 with an error payload is a real thing).
- [ ] **CORS** — what the same-origin policy is, why a browser request fails with a CORS error while `curl` succeeds, preflight (`OPTIONS`) requests, and that CORS is enforced by the *browser* and configured by the *server* (you usually can't "fix" it client-side).
- [ ] **Pagination, filtering & sorting** — offset/limit vs cursor pagination; reading `Link` headers or `next` cursors; why you must loop, not assume one response = all data.
- [ ] **Error handling & resilience** — mapping 4xx vs 5xx to different responses, respecting `429` + `Retry-After`, timeouts, and retries with backoff (concept).

### Should-Know Topics 🟡
- [ ] **Exploration tooling** — **curl** (the `-v`, `-H`, `-d`, `-X` you'll actually use), **Postman/Insomnia** for building and saving requests, and **HTTPie** as a friendlier curl.
- [ ] **Reading an API contract** — **OpenAPI/Swagger** specs and Swagger UI: how to find the endpoints, params, and response shapes without guessing.
- [ ] **HTTP caching for consumers** — `ETag`/`If-None-Match`, `Cache-Control`, and `304 Not Modified` — enough to not re-fetch needlessly.

### 🔗 Referenced, not taught here
- Applying this in a **React component** with loading/error/success UI → **React Phase 1, Stage 4**.
- The `fetch`/`await`/`try-catch` mechanics themselves → **JS Phase 1, Stage 3**.
- Supabase's specific auth keys (anon vs service_role) and how RLS guards them → **Supabase Phase 1, Stages 1 & 3**.

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me API authentication schemes — API keys, Bearer/JWT, session cookies, and OAuth 2.0 conceptually. Quiz me on where each credential goes in the request and the security trade-offs, and connect it to how Supabase ships a public anon key safely."
> 2. "Teach me CORS from the ground up — the same-origin policy, why a browser call fails but curl doesn't, and preflight requests. Give me a CORS error and make me diagnose whether it's a client or server fix."
> 3. "Teach me pagination (offset vs cursor), filtering, and consuming a large result set correctly, plus handling 429/Retry-After and retries. Make me write the loop that pages through a real API and stops correctly."
> 4. "Teach me to explore an API with curl and Postman and to read an OpenAPI/Swagger spec. Hand me an unfamiliar public API and make me authenticate and page through it using only its docs."

---

## Stage 4: Designing A REST API 🟡
**Goal of this stage:** Learn to *design* endpoints a consumer will thank you for — resource modeling, predictable URLs, correct verbs/status codes, versioning, and consistent error shapes.
**Estimated time:** 6–9 hours
**Milestone:** Given a domain (e.g. the Visual Life Archive: users, entries, media), you can design the full resource model and endpoint list — URLs, verbs, status codes, request/response bodies, pagination, versioning strategy, and a consistent error format — and justify each choice against REST conventions.

### Must-Know Topics 🔴
- [ ] **Resource modeling** — turning domain nouns into resources and collections; nesting (`/users/42/entries`) vs flat with query params, and when each is right.
- [ ] **URL, verb & status-code conventions** — plural collection names, no verbs in paths, returning `201 + Location` on create, `204` on delete, `200` vs `404` semantics; consistency over cleverness.
- [ ] **Request & response body design** — what to accept, what to return (return the created resource?), field naming consistency, and **partial update with PATCH vs full replace with PUT**.
- [ ] **Consistent error responses** — a single error shape (code + message + details), correct status codes for validation vs auth vs not-found; never a `200` wrapping an error.
- [ ] **Versioning** — URL versioning (`/v1/…`) vs header versioning, and why you version at all (not breaking existing consumers).

### Should-Know Topics 🟡
- [ ] **Pagination & filtering as a designer** — designing the query params and response envelope, cursor vs offset trade-offs from the *provider* side.
- [ ] **Idempotency & safety in design** — designing creates to tolerate retries (idempotency keys, concept), matching verbs to their guarantees.
- [ ] **Studying a world-class API** — read a great public API's reference (e.g. Stripe) to internalize what "good" feels like.

### 🔗 Referenced, not taught here
- Actually *implementing* a minimal API server (Express routes, request/response) → **JS Phase 1, Stage 8**.
- The auto-generated approach where the database *is* the API (PostgREST) → **Supabase Phase 1, Stage 2** — a useful contrast to hand-designing endpoints.

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me REST API resource modeling — turning a domain into resources, collections, and nesting decisions. Make me design the full resource model for the Visual Life Archive app (users, entries, media) and critique my choices."
> 2. "Teach me URL/verb/status-code conventions and consistent error-response design. Give me a badly designed endpoint list and make me fix every convention violation and justify it."
> 3. "Teach me API versioning and PATCH-vs-PUT update semantics. Quiz me on when a change is breaking and how versioning protects existing consumers."

---

## Stage 5: Testing REST APIs 🔴
**Goal of this stage:** Learn to test an API the way a QA engineer does — asserting on status, body, and schema; covering happy path, negative, auth, and boundary cases; and understanding contract testing — tool-agnostically, then mapped onto the tools you're learning.
**Estimated time:** 7–10 hours
**Milestone:** For a given endpoint you can write a test plan and tests that verify status codes, response body values, and schema; include negative cases (invalid input → 4xx, not 5xx), auth cases (missing/expired token → 401/403), and boundary cases; and explain what contract testing adds and when to reach for it.

### Must-Know Topics 🔴
- [ ] **What API testing is (and why it's below the UI)** — testing the contract directly: faster, more reliable, better business-logic coverage than E2E through a UI.
- [ ] **The three assertion layers** — **status code**, **response body** (specific fields via JSON path, not whole-body snapshots for dynamic data), and **schema/shape** (JSON Schema as a structural baseline).
- [ ] **Positive, negative, auth & boundary cases** — valid input → correct 2xx + data; invalid input → graceful **4xx with a helpful message, never a 5xx**; missing/expired/wrong token → 401/403; edge values at the limits.
- [ ] **Test data & isolation** — seeding state before a test and cleaning up after (setup/teardown), so tests don't depend on each other or on a flaky shared backend.
- [ ] **Contract testing (concept)** — consumer-driven contracts (e.g. Pact): why two independently-moving teams need explicit, automated compatibility checks, and how it differs from plain API testing.

### Should-Know Topics 🟡
- [ ] **Where API tests sit in the pyramid** — API vs integration vs E2E, and what belongs at each level.
- [ ] **Running API tests in CI** — the QAOps payoff: fast checks on every PR (connects to **GitHub Phase 1, Stage 5**).

### 🔗 Referenced, not taught here
- **Playwright's `request` fixture** for API tests → **JS Phase 1, Stage 7**.
- **Cypress `cy.request` / `cy.intercept`** (stubbing/spying network, seeding via request) → **Cypress Phase 1, Stage 4**.
- Testing a **Supabase** backend + RLS specifically → **Supabase Phase 1** (its testing stage).

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me what API testing is and the three assertion layers — status code, response body via JSON path, and JSON Schema validation. Give me an endpoint and make me write assertions at all three layers and explain why schema validation catches contract drift."
> 2. "Teach me designing positive, negative, auth, and boundary test cases for an endpoint, plus test data seeding and isolation. Make me write a full test plan for a create-and-fetch endpoint, including the failure cases most people forget."
> 3. "Teach me contract testing conceptually (consumer-driven contracts / Pact) and how it differs from ordinary API testing. Quiz me on when contract testing earns its keep versus when plain API tests are enough."

---

## 🏁 Final Milestone

You can pick up an unfamiliar REST API and, from first principles: read its docs/OpenAPI spec, authenticate, page through and filter its data, handle its errors and rate limits, and diagnose a CORS failure — all while explaining *why* each status code and header means what it does. You can **design** a clean REST API for a real domain (resources, URLs, verbs, status codes, versioning, consistent errors) and justify every choice. And you can **test** one thoroughly — status/body/schema assertions across positive, negative, auth, and boundary cases — and say where contract testing fits. At that point, Supabase's PostgREST API, a hand-built Express API, and any third-party API all read as instances of the same small set of ideas — and you're ready to apply them in the app (consuming), in your backend work (designing), and in your QAOps suites (testing).

---

## ⏭️ What's Out of Scope (For Now)

- **`fetch`/`async`/`await` mechanics** — owned by **JS Phase 1 Stage 3**; recalled lightly here, not re-taught.
- **Data-fetching UI states in a component** — owned by **React Phase 1 Stage 4**.
- **Implementing a server (Express) and Supabase/PostgREST specifics + RLS** — owned by **JS Phase 1 Stage 8** and **Supabase Phase 1**; this roadmap does the design/consume/test *thinking*, not those implementations.
- **Tool-specific test syntax** (Playwright `request`, Cypress `cy.request`/`cy.intercept`) — owned by **JS Phase 1 Stage 7** and **Cypress Phase 1 Stage 4**.
- **GraphQL in depth** — awareness only in Stage 2; a full GraphQL roadmap would be its own topic.
- **Real-time / streaming (WebSockets, SSE, Supabase Realtime)** — a different communication model; separate topic.
- **API gateways, rate-limit *implementation*, caching layers/CDNs, and production API ops** — provider-side infrastructure; a Phase 2 concern.
- **Performance/load testing of APIs** — a distinct QAOps layer (candidate for a later phase).
- **gRPC / Protocol Buffers** — RPC-style; awareness in Stage 2, no depth.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — "Teach me the HTTP request/response model and why HTTP is stateless — walk me through a real request line by line (method, path, headers, body, status). Quiz me on why statelessness forces us to send auth on every request."
2. Stage 1 — "Teach me HTTP methods and the safe / idempotent / cacheable properties. Quiz me hard: give me scenarios and make me pick the right verb and justify idempotency."
3. Stage 1 — "Teach me HTTP status code families and the common specific codes. Drill me with response scenarios and make me distinguish 400 vs 401 vs 403 vs 404 vs 422, and 500 vs 502 vs 503."
4. Stage 2 — "Teach me REST as an architectural style — resources, representations, statelessness, and the uniform interface — and why endpoints should be nouns. Make me redesign a verb-based API into a resource-based one and defend it."
5. Stage 2 — "Teach me the CRUD-to-HTTP-verb mapping with collection vs item URLs, and the Richardson Maturity Model. Give me several real API endpoints and make me place each on the RMM and justify it."
6. Stage 2 — "Teach me REST vs GraphQL vs RPC at a decision-making level — what each is good and bad at. Quiz me on which I'd pick for given scenarios, including my Supabase-backed app."
7. Stage 3 — "Teach me API authentication schemes — API keys, Bearer/JWT, session cookies, and OAuth 2.0 conceptually. Quiz me on where each credential goes and the security trade-offs, and connect it to how Supabase ships a public anon key safely."
8. Stage 3 — "Teach me CORS from the ground up — the same-origin policy, why a browser call fails but curl doesn't, and preflight requests. Give me a CORS error and make me diagnose whether it's a client or server fix."
9. Stage 3 — "Teach me pagination (offset vs cursor), filtering, and consuming a large result set correctly, plus handling 429/Retry-After and retries. Make me write the loop that pages through a real API and stops correctly."
10. Stage 3 — "Teach me to explore an API with curl and Postman and to read an OpenAPI/Swagger spec. Hand me an unfamiliar public API and make me authenticate and page through it using only its docs."
11. Stage 4 — "Teach me REST API resource modeling — turning a domain into resources, collections, and nesting decisions. Make me design the full resource model for the Visual Life Archive app and critique my choices."
12. Stage 4 — "Teach me URL/verb/status-code conventions and consistent error-response design. Give me a badly designed endpoint list and make me fix every convention violation and justify it."
13. Stage 4 — "Teach me API versioning and PATCH-vs-PUT update semantics. Quiz me on when a change is breaking and how versioning protects existing consumers."
14. Stage 5 — "Teach me what API testing is and the three assertion layers — status code, response body via JSON path, and JSON Schema validation. Give me an endpoint and make me write assertions at all three layers."
15. Stage 5 — "Teach me designing positive, negative, auth, and boundary test cases plus test data seeding and isolation. Make me write a full test plan for a create-and-fetch endpoint, including the failure cases most people forget."
16. Stage 5 — "Teach me contract testing conceptually (consumer-driven contracts / Pact) and how it differs from ordinary API testing. Quiz me on when contract testing earns its keep."

---

## 🔗 Cross-References To Your Other Roadmaps
- **JavaScript Phase 1** — Stage 3 owns `fetch`/async mechanics (prereq here); Stage 7 owns Playwright API-test tooling; Stage 8 owns the Express API implementation. This roadmap supplies the concepts underneath all three.
- **React Phase 1** — Stage 4 owns data-fetching UI states; this roadmap owns the API-consumer concepts it applies.
- **Cypress Phase 1** — Stage 4 owns `cy.request`/`cy.intercept`; and this roadmap **supersedes** Cypress's untaught "HTTP basics" prerequisite bullet (index supersede-flag).
- **Supabase Phase 1** — Stages 1–3 own PostgREST/keys/RLS; this roadmap uses Supabase as the concrete "real REST API" example and provides the generic REST/HTTP grounding its prereqs assume.
- **GitHub Phase 1** — Stage 5 (Actions II) is where Stage 5's API tests would run in CI.
