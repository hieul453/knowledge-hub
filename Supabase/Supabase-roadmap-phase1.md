# Learning Roadmap: Supabase — Phase 1 (The Platform)

**Goal:** Become genuinely comfortable with **Supabase the platform** — design a schema with **Row Level Security**, authenticate users (email + OAuth), store files with access policies, react to data with **Realtime**, run server-side logic in an **Edge Function**, and operate all of it as **version-controlled migrations via the CLI with a local dev stack** — plus seed and verify database state for automated tests. Understand *why* each service exists and where it fits, not just click through the dashboard.
**Context:** Three drivers weighted evenly — (1) **app backend** (the Visual Life Archive app: auth + data + media), (2) **general BaaS fluency** (know the whole platform and when to reach for each piece), and (3) **QAOps** (seeding/verifying a Supabase backend and testing RLS). Coverage is the *full* platform including dashboard, CLI, local development, and migrations depth.
**Time budget:** ~54–73 hrs of focused study + practice. No fixed schedule — estimates are in hours so you can pace yourself. Supabase rewards building: stand up a real project and wire each service as you go.
**Starting point:** Total beginner to Supabase. This roadmap is **self-contained** — it includes a light recall of SQL/relational basics where needed rather than assuming you've finished the SQL roadmap. Comfort with the SQL roadmap's early stages (querying, tables, constraints, joins) will make Stages 2–3 noticeably smoother, but isn't a hard gate.

---

## 🗺️ Overview

Supabase is a **backend-as-a-service built on a real, un-abstracted Postgres database** — that single fact organizes the whole platform. Every other service (Auth, Storage, Realtime, Edge Functions, the auto-generated API) is layered on top of, and secured by, that database. So this roadmap starts from the platform mental model and a project you can click around, then goes to the database layer and the auto-generated API that turns every table into an endpoint. The pivot — and the stage everyone underestimates — is **Row Level Security**: the database-level authorization that makes it *safe* to talk to Supabase directly from a client. From there it builds outward through Auth, Storage, and the reactive/serverless layers (Realtime + Edge Functions), then teaches you to **operate** it properly with the CLI, local Docker stack, and migrations, and finishes where your QAOps goal points: seeding, verifying, and **testing** a Supabase backend (including RLS policies) in CI. By the end you can run a real project's backend entirely on Supabase and explain why each piece behaves as it does.

---

## ⚠️ A Note On Your Starting Point (read this)

Two things worth internalizing before you start.

**First: security is not a late-stage add-on here — it's the core mental model.** In Supabase, your database is reachable from the client with a public key. That's *by design*, and it's only safe because **Row Level Security (RLS)** stands between the API and your data. The single most common — and most dangerous — Supabase mistake is shipping a table with RLS off or with a broken policy, which silently exposes every row to anyone with your project URL. Real CVEs and large-scale data leaks trace back to exactly this. So Stage 3 (RLS) is flagged 🧠 and weighted heavily; don't rush it, and adopt a "deny by default, prove access" habit from the start.

**Second: this roadmap deliberately re-covers a little SQL.** You chose a self-contained build, so Stages 1–2 include a light recall of tables/queries/relationships. If you've done the SQL roadmap, treat those as review and move faster. If you haven't, you'll have enough to be productive — but the SQL roadmap remains the deeper source for the *database engine* itself (joins, transactions, schema design), and this roadmap owns everything Supabase adds *on top*.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **Basic SQL & relational concepts** 🔴 — tables, rows, `SELECT`/`INSERT`/`UPDATE`/`DELETE`, primary/foreign keys. A light recall is built into Stages 1–2, so this isn't a hard gate; your SQL roadmap's Stages 1–4 are the fuller source if you want it. — est. **light recall included**
- [ ] **A free Supabase account** 🔴 — sign up and create a throwaway project so you have somewhere to click and query from minute one. — est. **15 min**
- [ ] **Node.js + npm** 🔴 — for `supabase-js` and the Supabase CLI. You have this from your JS track. — est. **0–1 hr**
- [ ] **JavaScript async basics (`async`/`await`, promises)** 🔴 — every `supabase-js` call is async; your JS roadmap Stages 1–3 cover this. — est. *(covered by your JS roadmap)*
- [ ] **Docker Desktop** 🟡 — required for the local development stack in Stage 7 (the CLI runs the whole Supabase stack in containers). Install it before Stage 7, not necessarily now. — est. **30 min**
- [ ] **Terminal + VS Code** 🟡 — you already have these from your other tracks. — est. **0–30 min**
> ✅ Skip any you already have. The only thing that will genuinely slow you down later is missing Docker for Stage 7 — install it before you get there.

---

## Stage 1: What Supabase Is — Platform Mental Model & Setup
**Goal of this stage:** Understand *why* Supabase is "a real Postgres with services on top," navigate the dashboard, and get oriented in a project — including the keys that everything else depends on.
**Estimated time:** 4–6 hrs
**Milestone:** You can create a project, explain each dashboard section (Table Editor, SQL Editor, Auth, Storage, etc.), articulate the difference between the **publishable/anon key** and the **service_role key** (and why one is safe to ship and the other never is), and run your first query in the SQL Editor — and state, in plain language, "Postgres does X; Supabase adds Y on top."

### Must-Know Topics 🔴
- [ ] **Supabase = managed Postgres + a service layer** — a **backend-as-a-service**: a full Postgres database with **Auth**, **Storage**, **Realtime**, **Edge Functions**, and an **auto-generated API** built on top; Supabase does *not* abstract Postgres away — you get the real thing
- [ ] **Why this model (vs. Firebase / vs. rolling your own backend)** — relational + SQL vs. NoSQL; "no server code required" because the database and its policies *are* the backend; open-source and portable
- [ ] **Project anatomy & the dashboard** — Table Editor vs. **SQL Editor**, the Auth / Storage / Database / Edge Functions sections; the project URL
- [ ] **The keys** 🔴 — the **anon / publishable key** (safe to ship, RLS-guarded) vs. the **service_role / secret key** (bypasses RLS — server-only, never in client code); this distinction underpins every security decision later
- [ ] **Light SQL recall** — tables/rows/columns and a first `SELECT` in the SQL Editor (fuller depth lives in your SQL roadmap)

### Should-Know Topics 🟡
- [ ] The underlying open-source pieces by name — Postgres, GoTrue (Auth), PostgREST (the auto-API), Realtime, Storage API, Studio (the dashboard) — so the docs make sense
- [ ] `database.new` and how fast a project spins up; free-tier limits at a glance

### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what Supabase is — a real Postgres database with Auth, Storage, Realtime, Edge Functions, and an auto-generated API layered on top — and how it compares to Firebase and to building my own backend. Quiz me until I can explain where Postgres ends and Supabase begins."
> 2. "Walk me through a Supabase project and dashboard, and drill me hard on the difference between the anon/publishable key and the service_role key — which is safe to ship and why. Verify I understand the security implication of each."

---

## Stage 2: The Database Layer — Tables, Relationships & the Auto-Generated API
**Goal of this stage:** Model data in Supabase and understand the thing that makes it a *backend* — that every table automatically becomes a queryable API, consumed through the `supabase-js` client.
**Estimated time:** 7–9 hrs
**Milestone:** You can design a small relational schema in Supabase (Table Editor *and* SQL Editor), define foreign-key relationships, and read/write it from `supabase-js` — including filtering and querying related tables — and explain how PostgREST turns your schema into an API.

### Must-Know Topics 🔴
- [ ] **Designing tables in Supabase** — creating tables, choosing data types, primary keys (**identity vs. `uuid`**), and defaults; light recall of schema design (deeper in your SQL roadmap)
- [ ] **Relationships** — foreign keys, one-to-many, and **many-to-many via a join table** (e.g. the classic movies↔categories / entries↔tags shape)
- [ ] **The auto-generated Data API (PostgREST)** — how *every* table in an exposed schema becomes a REST endpoint automatically; this is *why* you don't write a server
- [ ] **The `supabase-js` client** — `supabase.from('table').select()/insert()/update()/delete()`, filters (`.eq`, `.in`, etc.), ordering, and **querying related tables** (embedded resources via FK); that `.insert()` returns rows by default and how that interacts with RLS
- [ ] **`grant` vs. RLS (first look)** — a role must be *granted* access to a table for the API to reach it at all; RLS then decides *which rows* (full depth in Stage 3)

### Should-Know Topics 🟡
- [ ] The **GraphQL API** (`pg_graphql`) — that it exists as an alternative to REST; when you'd reach for it
- [ ] **Views** — saving a complex query as a reusable virtual table, and the `security_invoker` caveat for RLS
- [ ] Schemas — the `public` schema you live in by default, and why a dedicated `api` schema can be a cleaner exposure surface

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me designing tables and relationships in Supabase — data types, primary keys (identity vs uuid), and one-to-many/many-to-many with a join table. Make me model a small schema both in the Table Editor and in SQL."
> 2. "Teach me the auto-generated Data API (PostgREST) and the supabase-js client — select/insert/update/delete, filters, and querying related tables — and how a role is granted access to a table before RLS even applies. Give me a schema and make me read and write it from the client."

---

## Stage 3: Row Level Security & the Auth-to-Data Security Model 🧠
**Goal of this stage:** This is the deep, critical stage. Internalize **Row Level Security** — the database-level authorization that makes it safe to talk to Supabase from a client — and how a user's identity flows from Auth into your policies.
**Estimated time:** 9–12 hrs (slow down here — this is the stage that protects, or leaks, all your data)
**Milestone:** You can enable RLS, write correct `SELECT`/`INSERT`/`UPDATE`/`DELETE` policies using `auth.uid()`, explain `USING` vs. `WITH CHECK` and the `anon`/`authenticated`/`service_role` roles, articulate *why* the anon key is safe once RLS is on, and predict whether a given query returns rows for a given user before you run it.

### Must-Know Topics 🔴
- [ ] **What RLS is and why it's the core security model** — policies act as an implicit `WHERE` clause the database appends to *every* query; with RLS on and no policy, a table returns **nothing** (safe by default); with RLS off, your anon key exposes every row (the #1 Supabase security failure)
- [ ] **Writing policies** — `CREATE POLICY`, `FOR SELECT/INSERT/UPDATE/DELETE`, and **`USING` (which existing rows are visible/affected) vs. `WITH CHECK` (what new/updated rows are allowed)**; why an `UPDATE` policy usually needs a matching `SELECT` policy
- [ ] **The roles** — `anon`, `authenticated`, `service_role`; using the **`TO` clause** to scope policies to a role, and why `service_role` bypasses RLS
- [ ] **Auth → data linkage** — **`auth.uid()`** and `auth.jwt()` helpers; the everyday `auth.uid() = user_id` ownership policy; why you must *not* trust user-editable `user_metadata` in a policy
- [ ] **Why the publishable key is safe to ship** — because RLS enforces access at the database, independent of the client; "defense in depth" even against direct API access

### Should-Know Topics 🟡
- [ ] **Testing/impersonating users** — Supabase Studio's user-impersonation / policy tester to check a policy as a specific user (sets up Stage 8's automated RLS tests)
- [ ] **RLS performance basics** — indexing the columns your policies filter on (e.g. `user_id`), wrapping `auth.uid()` in a `select`, and always adding `authenticated` to rule out `anon` cheaply
- [ ] **Multi-tenant / team patterns (awareness)** — `team_id`-based access via a membership table; security-definer helper functions to avoid recursive RLS

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Row Level Security in Supabase from the ground up — why it's the core security model, that RLS-on-no-policy denies everything, and how to write SELECT/INSERT/UPDATE/DELETE policies with USING vs WITH CHECK. Quiz me hard: give me a table and a user and make me predict which rows a query returns, and make me write the policy."
> 2. "Teach me how auth identity flows into RLS — auth.uid()/auth.jwt(), the anon/authenticated/service_role roles and the TO clause, and why the publishable key is safe to ship once RLS is on. Drill me on the ownership policy pattern and on why I must not trust user_metadata in a policy."

---

## Stage 4: Authentication In Depth
**Goal of this stage:** Use Supabase Auth as a full auth system — sign users up and in across multiple methods, manage sessions, and connect auth users to your own tables.
**Estimated time:** 7–9 hrs
**Milestone:** You can implement email/password *and* an OAuth provider (plus magic link / OTP awareness), manage the session lifecycle (`getSession` / `onAuthStateChange` / refresh / sign-out), link `auth.users` to a `profiles` table via a trigger, and explain how the issued JWT drives the RLS policies from Stage 3.

### Must-Know Topics 🔴
- [ ] **What Supabase Auth (GoTrue) is** — a JWT-based auth service that stores users in a dedicated `auth` schema and integrates directly with RLS; authentication (who you are) vs. authorization (what you can touch)
- [ ] **Email/password** — sign-up, email confirmation, sign-in, password reset
- [ ] **OAuth / social login & passwordless** — configuring a provider (Google/GitHub/etc.), plus **magic link** and **email/phone OTP** as alternatives
- [ ] **Sessions & JWTs** — `getSession` vs. `getUser` (and why `getUser` is the trustworthy one server-side), `onAuthStateChange`, access vs. refresh tokens, session persistence, sign-out
- [ ] **Linking auth to your data** — the pattern of a `profiles` table keyed to `auth.users.id`, populated by a trigger on user creation; the FK that ties everything to `auth.uid()`

### Should-Know Topics 🟡
- [ ] **Server-side auth / SSR (awareness)** — cookie-based sessions for frameworks like Next.js/SvelteKit; that native mobile (Expo) uses a storage adapter + deep links (ties to your RN roadmap)
- [ ] **MFA & anonymous sign-ins** — that TOTP/phone MFA and anonymous users exist and roughly when to use them
- [ ] **Admin API** — `auth.admin.createUser` (service-role) for seeding test users (feeds Stage 8)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Supabase Auth — email/password with confirmation, adding an OAuth provider, and magic link/OTP — plus the session lifecycle (getSession vs getUser, onAuthStateChange, refresh tokens, sign-out). Make me reason through a full sign-up-to-signed-in flow."
> 2. "Teach me how Auth connects to my data — the auth.users table, a profiles table linked by a trigger, and how the issued JWT powers the auth.uid() RLS policies from the RLS stage. Verify I understand the end-to-end path from login to a row-scoped query."

---

## Stage 5: Storage — Files, Buckets & Access Policies
**Goal of this stage:** Store and serve files (the app's photos) securely — buckets, uploads, and the RLS policies that guard objects.
**Estimated time:** 5–7 hrs
**Milestone:** You can create public and private buckets, upload and download files with `supabase-js`, write **Storage RLS policies** on `storage.objects`, and generate signed URLs for private files — and explain when to use a public URL vs. a signed URL, and the common upload pitfalls.

### Must-Know Topics 🔴
- [ ] **Buckets & objects** — creating buckets, **public vs. private**, the `storage.objects` table that metadata lives in
- [ ] **Uploading & downloading** — `supabase.storage.from(bucket).upload()/download()`; organizing paths (e.g. per-user folders)
- [ ] **Storage access control is RLS** — policies on `storage.objects` (no uploads allowed without a policy); scoping access to the owner; that `service_role` bypasses storage RLS too
- [ ] **Serving files** — **public URLs** vs. **signed URLs** (time-limited access to private objects); when each is appropriate
- [ ] **Image transformations** — on-the-fly resizing/optimization for a photo grid (awareness + basic use)

### Should-Know Topics 🟡
- [ ] **The upload-body gotcha** — turning a file/blob (or a mobile `file://` URI) into an uploadable body; the classic React Native pitfall (cross-refs your RN roadmap's Stage 5)
- [ ] **CDN caching & resumable uploads** — that large files and caching are handled, at an awareness level

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Supabase Storage — buckets (public vs private), uploading and downloading files with supabase-js, and organizing per-user paths. Make me build an 'upload a photo and display it' flow."
> 2. "Teach me Storage access control as RLS on storage.objects, plus public vs signed URLs and image transformations. Quiz me on writing a policy that lets a user access only their own files, and on when to use a signed URL."

---

## Stage 6: Realtime & Edge Functions — The Reactive & Serverless Layers
**Goal of this stage:** Add the two services that go beyond request/response — live data with **Realtime**, and server-side logic with **Edge Functions** — and know when each is the right tool.
**Estimated time:** 8–11 hrs
**Milestone:** You can subscribe to live data changes (respecting RLS), explain Realtime's three modes, write and deploy a Deno Edge Function that runs server-side logic (using the service role or a secret safely), and articulate when you genuinely need an Edge Function vs. a direct client query.

### Must-Know Topics 🔴
- [ ] **Realtime — the three capabilities** — **Postgres Changes** (stream inserts/updates/deletes), **Broadcast** (low-latency messages between clients), and **Presence** (who's online / shared state); subscribing with `supabase.channel(...)`
- [ ] **Realtime + RLS + replication** — that Realtime is opt-in per table (enable replication), that `REPLICA IDENTITY FULL` is needed for old row data, and that **Realtime respects RLS only when configured to** (a common security gap)
- [ ] **What Edge Functions are** — **Deno/TypeScript serverless functions** at the edge; *why* you need server-side code (hiding secrets, calling third-party APIs like Stripe, webhooks, work that must not run on the client)
- [ ] **Writing & deploying a function** — `supabase functions new`, the handler shape, `supabase functions serve` locally, `supabase functions deploy`; accessing your DB/auth from inside a function with zero config
- [ ] **Secrets in functions** — storing credentials as project secrets / env vars, never hardcoding them

### Should-Know Topics 🟡
- [ ] **Database Functions & Triggers (awareness)** — Postgres-side logic (`SECURITY DEFINER`, triggers) and how it differs from Edge Functions; the `profiles`-on-signup trigger you met in Stage 4 is one
- [ ] **Database Webhooks** — firing an HTTP call (often to an Edge Function) on row changes
- [ ] **Function constraints** — cold starts, keep them short/idempotent, treat Postgres as a pooled remote

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Supabase Realtime — Postgres Changes, Broadcast, and Presence — how to subscribe with channels, how replication is enabled per table, and the critical point that Realtime only respects RLS when configured to. Quiz me on choosing the right mode and on the security gap."
> 2. "Teach me Supabase Edge Functions — Deno/TypeScript serverless functions, why and when I need server-side logic, writing/serving/deploying one, accessing the DB from inside it, and handling secrets. Make me decide, for several scenarios, whether to use an Edge Function or a direct client query."

---

## Stage 7: Local Dev, CLI, Migrations & Environments — Operating It Properly 🧠
**Goal of this stage:** Stop clicking in the dashboard and start operating Supabase like an engineer — a local stack, version-controlled schema migrations, and clean environment management.
**Estimated time:** 8–10 hrs
**Milestone:** You can run the full Supabase stack locally with the CLI, capture schema changes as **migration files** (hand-written or via `db diff`), seed the local database deterministically, link and **push** migrations to a hosted project, and manage config/secrets across environments — and explain why migrations-in-git beats dashboard clicking.

### Must-Know Topics 🔴
- [ ] **The Supabase CLI + local stack** — `supabase init`, `supabase start` (Docker) to run Postgres + Auth + Storage + Realtime + Edge Functions + Studio locally; `supabase status`; `supabase stop`
- [ ] **Migrations** — database changes as version-controlled files in `supabase/migrations`; writing them by hand *or* generating with **`supabase db diff`**; the shadow-database idea; **declarative schema** files as the modern option
- [ ] **`supabase db reset` & seeding** — recreate the local DB from migrations + a `seed.sql` to get a known state on demand (this is the backbone of reliable testing in Stage 8)
- [ ] **Linking & deploying** — `supabase link`, `supabase db push` to apply migrations to the hosted project; keeping local and remote in sync; `config.toml` for project config (including enabling Auth providers locally)
- [ ] **Environments & secrets** — `.env` substitution for the CLI, `EXPO_PUBLIC_`/publishable vs. secret values, keeping secrets out of git (ties to your Git roadmap)

### Should-Know Topics 🟡
- [ ] **Branching / preview environments** — ephemeral databases per PR (awareness); how this pairs with CI
- [ ] **Generating types** — `supabase gen types` to produce TypeScript types from your schema (a strong bridge to your TypeScript roadmap)
- [ ] **Local vs. hosted differences** — the local stack is for dev/testing only, never exposed; some dashboard settings only exist remotely

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the Supabase CLI and local development stack — init/start/status/stop with Docker, and what services run locally. Then teach me migrations: capturing schema changes as version-controlled files, db diff, and declarative schema. Verify I understand why migrations-in-git beat clicking in the dashboard."
> 2. "Teach me db reset + seed.sql for deterministic local state, linking and db push to a hosted project, and managing config/secrets across environments. Make me walk a schema change from local migration to deployed, and quiz me on keeping secrets out of git."

---

## Stage 8: QAOps — Testing Against Supabase, Seeding & Verifying State
**Goal of this stage:** The QAOps payoff. Prove your backend works — seed known state, verify it, and **test your RLS policies** — both in SQL and through the client, wired into CI.
**Estimated time:** 6–9 hrs
**Milestone:** You can write **pgTAP** tests that verify schema and RLS policies (run with `supabase test db`), write application-level tests through `supabase-js` that seed via the service role and assert an authenticated user only sees their own rows, and run both in GitHub Actions against a local stack — and explain why testing *denied* access matters as much as allowed access.

### Must-Know Topics 🔴
- [ ] **Two testing approaches** — **database-level** (pgTAP, SQL, transaction-isolated with `BEGIN`/`ROLLBACK`) vs. **application-level** (through `supabase-js` in your JS test framework, end-to-end but not transaction-isolated)
- [ ] **pgTAP for schema + RLS** — `supabase test db`, `plan()`/`finish()`, helpers like `has_column`, `policies_are`, and the community `tests.create_supabase_user` / `tests.authenticate_as` helpers to assert a policy blocks the wrong user
- [ ] **Testing RLS the right way** — verify all three cases for every protected table: anon (rejected/empty), correct user (sees own rows), *different* user (**zero rows**); why "it works when I'm logged in as me" is a false pass
- [ ] **Seeding & verifying with the service role** — use the **secret/service_role** key to set up state (bypassing RLS), then assert with an **anon/authenticated** client; unique IDs per test so app-level tests stay independent
- [ ] **Running tests in CI** — `supabase/setup-cli` + `supabase start` + `supabase test db` in GitHub Actions (ties directly to your GitHub Actions roadmap, Stage 5)

### Should-Know Topics 🟡
- [ ] **Teardown strategy** — pgTAP's `ROLLBACK` per test for clean isolation; `db reset`/`TRUNCATE` for app-level suites (recall of your SQL roadmap's transactions stage)
- [ ] **`rls_enabled('public')`** — a single assertion that every table in a schema has RLS on — a cheap safety net against the #1 mistake
- [ ] **Testing Edge Functions & Storage** — invoking a function and asserting storage-policy behavior (awareness)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me testing a Supabase database — the two approaches (pgTAP in SQL with BEGIN/ROLLBACK vs. application-level through supabase-js) — and writing pgTAP tests for schema and RLS policies with supabase test db. Make me write a test that proves a user cannot read another user's rows, and drill me on why testing denied access matters."
> 2. "Teach me seeding and verifying state for tests — using the service_role key to set up data, asserting with an authenticated client, unique IDs for isolation — and running supabase test db in GitHub Actions. Have me design a CI test pipeline that spins up the local stack and runs RLS tests."

---

## 🏁 Final Milestone
You can stand up and operate a complete, secure backend entirely on Supabase: a relational schema exposed through the auto-generated API and **locked down with correct Row Level Security**, users authenticated via email and OAuth with sessions linked to their data, photos stored in policy-guarded buckets, live updates via Realtime, and server-side logic in a deployed Edge Function — all managed as **version-controlled migrations through the CLI with a local dev stack**, and **seeded, verified, and RLS-tested in CI**. And — the "understand it" part — you can explain to another engineer *why* Supabase can safely ship a public key (RLS), *why* each service exists and when to reach for it, and *why* an RLS test must prove denied access, not just allowed access. At that point you're ready to add TypeScript types (`supabase gen types` → your TS roadmap), wire this backend into the Visual Life Archive app, and take on advanced RLS/performance and self-hosting as clearly-scoped next steps.

---

## ⏭️ What's Out of Scope (For Now)
- **Deep Postgres/SQL engine** — advanced querying, transactions internals, and schema-design theory are owned by your **SQL Phase 1** roadmap. This roadmap does light recall and builds the platform on top.
- **Advanced RLS at scale** — complex multi-tenant RBAC, RLS performance tuning with `EXPLAIN`, and security-definer optimization patterns. You get the foundations + awareness here; depth is a Phase 2.
- **Self-hosting Supabase** — running the full stack (Docker Compose, Kong, GoTrue, etc.) on your own infra. Awareness only; the local CLI stack is for dev/testing, *not* self-hosting.
- **`pgvector` / AI & vector embeddings** — Supabase's vector/AI toolkit is a distinct track; excluded to keep the platform focus.
- **Advanced Postgres extensions** — PostGIS, `pg_cron`, `pg_net`, Vault (beyond secrets awareness) — situational, learn when a project needs them.
- **Production ops at scale** — read replicas, connection pooling depth (Supavisor tuning), observability, point-in-time recovery, scaling. Relevant when you run production, not when you're learning the platform.
- **Framework-specific SSR auth deep-dives** — Next.js server-component auth, cookie helpers per framework. Awareness in Stage 4; the deep integration is per-framework and separate.
- **Management API & CI/CD for the platform itself** — programmatic project/org management. A Phase 2 automation topic.

---

## 🔗 Cross-References To Your Other Roadmaps

- **SQL & Relational Databases Phase 1** owns the Postgres/SQL *engine*; this roadmap does light recall and builds Supabase's services on top. **This roadmap fulfills the "RLS in depth" deferral** that the SQL roadmap's Stage 7 and Out-of-Scope explicitly pointed at "a Supabase/auth roadmap" — so it **supersedes** that out-of-scope note. (Index maintenance: add a cross-reference flag, the way TypeScript Stage 6 supersedes Cypress's TS-custom-commands out-of-scope note.)
- **React Native + Expo Phase 1** consumes Supabase from the *mobile client* (its Stage 5–6: `supabase-js` in Expo, email/password auth, basic CRUD, RLS scoped to `auth.uid()`, Storage upload from a device URI) and lists **Realtime and Edge Functions as out of scope**. This roadmap is the **deeper, broader platform source** — it covers those excluded services and treats RLS/Auth/Storage in full — so it **supersedes the RN roadmap's Supabase intro on depth**; the RN roadmap remains the "applied in a mobile app" consumer.
- **GitHub Phase 1 (Stage 5, Actions II)** is where the Stage 8 pgTAP/RLS tests and `supabase test db` actually run in CI.
- **Git Phase 1** — migrations live in version control; Stage 7's "migrations-in-git" habit is your Git workflow applied to the database.
- **TypeScript Phase 1** — `supabase gen types` (Stage 7) generates types from your schema, a clean bridge into typing the app and its tests.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Platform model: "Teach me what Supabase is — a real Postgres database with Auth, Storage, Realtime, Edge Functions, and an auto-generated API layered on top — and how it compares to Firebase and to building my own backend. Quiz me until I can explain where Postgres ends and Supabase begins."
2. Stage 1 — Project & keys: "Walk me through a Supabase project and dashboard, and drill me hard on the difference between the anon/publishable key and the service_role key — which is safe to ship and why. Verify I understand the security implication of each."
3. Stage 2 — Tables & relationships: "Teach me designing tables and relationships in Supabase — data types, primary keys (identity vs uuid), and one-to-many/many-to-many with a join table. Make me model a small schema both in the Table Editor and in SQL."
4. Stage 2 — Auto-API & client: "Teach me the auto-generated Data API (PostgREST) and the supabase-js client — select/insert/update/delete, filters, and querying related tables — and how a role is granted access to a table before RLS even applies. Give me a schema and make me read and write it from the client."
5. Stage 3 — RLS core: "Teach me Row Level Security in Supabase from the ground up — why it's the core security model, that RLS-on-no-policy denies everything, and how to write SELECT/INSERT/UPDATE/DELETE policies with USING vs WITH CHECK. Quiz me hard: give me a table and a user and make me predict which rows a query returns, and make me write the policy."
6. Stage 3 — Auth→data: "Teach me how auth identity flows into RLS — auth.uid()/auth.jwt(), the anon/authenticated/service_role roles and the TO clause, and why the publishable key is safe to ship once RLS is on. Drill me on the ownership policy pattern and on why I must not trust user_metadata in a policy."
7. Stage 4 — Auth flows: "Teach me Supabase Auth — email/password with confirmation, adding an OAuth provider, and magic link/OTP — plus the session lifecycle (getSession vs getUser, onAuthStateChange, refresh tokens, sign-out). Make me reason through a full sign-up-to-signed-in flow."
8. Stage 4 — Auth↔data linkage: "Teach me how Auth connects to my data — the auth.users table, a profiles table linked by a trigger, and how the issued JWT powers the auth.uid() RLS policies. Verify I understand the path from login to a row-scoped query."
9. Stage 5 — Storage: "Teach me Supabase Storage — buckets (public vs private), uploading/downloading with supabase-js, and organizing per-user paths. Make me build an 'upload a photo and display it' flow."
10. Stage 5 — Storage policies: "Teach me Storage access control as RLS on storage.objects, plus public vs signed URLs and image transformations. Quiz me on a policy that lets a user access only their own files, and on when to use a signed URL."
11. Stage 6 — Realtime: "Teach me Supabase Realtime — Postgres Changes, Broadcast, and Presence — subscribing with channels, enabling replication per table, and that Realtime only respects RLS when configured to. Quiz me on choosing the right mode and on the security gap."
12. Stage 6 — Edge Functions: "Teach me Supabase Edge Functions — Deno/TypeScript serverless functions, why and when I need server-side logic, writing/serving/deploying one, accessing the DB from inside it, and handling secrets. Make me decide, per scenario, Edge Function vs. direct client query."
13. Stage 7 — CLI & migrations: "Teach me the Supabase CLI and local stack — init/start/status/stop with Docker — then migrations: version-controlled files, db diff, and declarative schema. Verify I understand why migrations-in-git beat dashboard clicking."
14. Stage 7 — Deploy & environments: "Teach me db reset + seed.sql for deterministic local state, linking and db push to a hosted project, and managing config/secrets across environments. Make me walk a schema change from local migration to deployed."
15. Stage 8 — pgTAP & RLS tests: "Teach me testing a Supabase database — pgTAP in SQL (BEGIN/ROLLBACK) vs application-level through supabase-js — and writing pgTAP tests for schema and RLS with supabase test db. Make me write a test that proves a user cannot read another user's rows, and drill me on why testing denied access matters."
16. Stage 8 — Seed/verify + CI: "Teach me seeding and verifying state for tests — service_role to set up, authenticated client to assert, unique IDs for isolation — and running supabase test db in GitHub Actions. Have me design a CI test pipeline that spins up the local stack and runs RLS tests."
