# Learning Roadmap: Cross-Cutting Concepts — Authentication & Secrets — Phase 1

**Goal:** Understand two concepts that touch every part of your app: how **authentication** works (how a user logs in and stays logged in, and how the backend knows which data is theirs), and how **environment variables & secrets** work (which config is safe to ship in the app vs. must never leave the server). You won't implement auth from scratch — Supabase does that — but you'll understand it well enough to use it correctly and safely.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). These are "Group 4" cross-cutting concepts — learn them alongside your backend/Supabase work, not in isolation.
**Time budget:** ~8–12 hrs of focused study. Concept-heavy, light on hands-on until Stage 3–4.
**Starting point:** Total beginner. This roadmap is conceptual first (how auth works in general), then applied to your exact stack (Supabase Auth on Expo).

---

## 🗺️ Overview

Every app with user accounts has to answer three questions: *who are you* (authentication), *what are you allowed to see* (authorization), and *how do we remember you between requests* (sessions or tokens). This roadmap builds that mental model from the ground up, then shows how **Supabase Auth** handles all of it for you — including where the "proof of login" lives on your phone. The second half covers **environment variables and secrets**: the config that connects your app to Supabase, and the single most important security lesson for a client app — *anything shipped to the phone is not secret*, so you'll learn exactly which keys are safe to embed and which must stay server-side. The payoff is being able to wire up login and configuration for your app without accidentally leaking anything.

---

## ⚠️ A Note On What You're Learning (read this)

You are **not** learning to build an auth server, hash passwords, or write cryptography — Supabase does all of that. You're learning the *concepts* well enough to (a) use Supabase Auth correctly, (b) reason about where the login token lives and why, and (c) never leak a secret. When a topic here has a "you won't implement this" flavor, that's intentional — understanding beats reinventing.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **JavaScript async + HTTP basics** 🟡 — from your JS roadmap Stage 3 (fetch, request/response, async/await). Auth is fundamentally a sequence of HTTP requests. — est. *(covered in JS roadmap)*
- [ ] **What an API / client–server exchange is** 🟡 — the idea that your app sends requests to a backend and gets responses. — est. 1 hr if new
- [ ] **`.gitignore` basics** 🟢 — from Git roadmap Stage 2; you'll use it to keep secrets out of version control. — est. *(covered in Git roadmap)*
- [ ] **React core concepts** 🟢 — only for Stage 3's "protected routes / auth state" part; not needed earlier. — est. *(covered in React roadmap)*
> ✅ Stages 1–2 are pure concept and need almost no setup — you can start today.

---

## Stage 1: Authentication Fundamentals — The Mental Model
**Goal of this stage:** Understand what authentication actually is and the universal shape of a login flow, before any specific technology.
**Estimated time:** 2–3 hrs
**Milestone:** You can clearly explain **authentication vs authorization**, and trace a login flow end to end: credentials → server verifies → issues proof of identity → client sends that proof on every later request.

### Must-Know Topics 🔴
- [ ] **Authentication vs authorization** — *who you are* vs *what you're allowed to do*; two different questions people constantly conflate
- [ ] **The universal login flow** — user submits credentials → server verifies them → server issues some *proof of identity* → client stores it → client attaches it to future requests
- [ ] **Why this is needed at all** — HTTP is **stateless**: the server forgets you between requests, so every request must carry proof of who you are
### Should-Know Topics 🟡
- [ ] **Passwords are never stored in plain text** — servers store a *hash*; you won't implement this (Supabase does), but know it's why "we can't see your password" is true
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me authentication vs authorization with clear examples, and the universal login flow — credentials, verification, proof of identity, and sending that proof on later requests. Quiz me until I can explain each step and why HTTP being stateless makes it necessary."

---

## Stage 2: Sessions vs Tokens (and JWTs)
**Goal of this stage:** Understand the two ways apps "remember" a logged-in user, and what a JWT actually is — the format your app will use.
**Estimated time:** 2–3 hrs
**Milestone:** You can explain the difference between session-based and token-based auth, name the three parts of a JWT and what each does, and explain why you must never put a secret in a JWT payload or store a token carelessly.

### Must-Know Topics 🔴
- [ ] **Session-based auth (stateful)** — server stores a session record; client holds only a **session ID**, usually in a cookie; server looks it up on each request
- [ ] **Token-based auth (stateless)** — server issues a **signed token** the client stores and sends back; server verifies the *signature* instead of doing a lookup. This is what Supabase/mobile apps use.
- [ ] **JWT structure** — `header.payload.signature`: the **payload** carries claims (user id, expiry) and is only base64-encoded, so it's **readable by anyone** → never put secrets in it; the **signature** proves the token wasn't tampered with
- [ ] **Access vs refresh tokens** — short-lived access token + longer-lived refresh token (why: limit the damage if a token leaks)
### Should-Know Topics 🟡
- [ ] **Where tokens live on the client** — why plain `localStorage` (web) is risky (XSS), and why mobile apps use secure device storage (covered concretely in Stage 3)
- [ ] **Why mobile/APIs favor tokens** — no cookie/browser ergonomics; a token in an `Authorization` header is simpler
### Nice-to-Know Topics 🟢
- [ ] **CSRF vs XSS** at a high level — the two attack classes each storage choice trades off against
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me session-based vs token-based authentication — stateful server sessions with a session-ID cookie vs stateless signed tokens. Quiz me on the trade-offs."
> 2. "Teach me what a JWT is — header, payload, signature — and why the payload is readable (never a secret store) while the signature proves integrity. Include access vs refresh tokens. Make me explain each part back."

---

## Stage 3: Auth in Your App — Supabase Auth on Expo
**Goal of this stage:** See how Supabase Auth does everything from Stages 1–2 for you, and understand where the login lives on the device and how your data stays private.
**Estimated time:** 2–3 hrs
**Milestone:** You can describe, end to end, how login works in the Visual Life Archive app with Supabase Auth — where the session/token lives on the phone, and how the database ensures each user only sees their own moments.

### Must-Know Topics 🔴
- [ ] **Supabase Auth does the heavy lifting** — sign up / sign in / sign out, issuing JWTs, and persisting the session, all handled for you via `supabase-js`
- [ ] **The session object & persistence** — how the client keeps you logged in across app restarts (the session is stored and auto-refreshed)
- [ ] **How your data stays private (RLS, at a concept level)** — Postgres **Row-Level Security** ties `auth.uid()` to rows, so a logged-in user can only read their own records. This is *why* it's safe to talk to the database directly from the app. (Deep RLS policy-writing belongs in the future Supabase roadmap — concept only here.)
- [ ] **Storing the session securely on device** — on mobile, sensitive session data belongs in secure storage (Expo **SecureStore** → iOS Keychain / Android Keystore), not plain unprotected storage
### Should-Know Topics 🟡
- [ ] **Protected routes / auth state** — gating screens on whether a session exists (typically via React context) so signed-out users can't reach the app's inner screens
- [ ] **Email verification & social login exist** — Supabase supports email confirmation and OAuth providers (Google/Apple); awareness now, setup later
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me how Supabase Auth works in an Expo React Native app — sign up/in/out, the session object, and how it persists login across restarts. Relate each piece back to the sessions/tokens concepts I learned. Quiz me on where the token lives."
> 2. "Teach me, at a concept level, how Row-Level Security makes it safe to query the database directly from the app so each user only sees their own data, and why the session should be stored in secure device storage. Make me explain the end-to-end privacy story for my app."

---

## Stage 4: Environment Variables & Secrets
**Goal of this stage:** Understand configuration and secrets — and the one client-app security lesson that trips up every beginner.
**Estimated time:** 2–3 hrs
**Milestone:** You can correctly classify every key in your app as *safe to ship to the client* vs *server-only*, set up a working `.env` with `EXPO_PUBLIC_` variables, and keep it out of Git.

### Must-Know Topics 🔴
- [ ] **What env vars are & why** — keep configuration *out* of code so values can differ per environment (dev vs prod) and change without editing source
- [ ] **`.env` files & how they load** — Node reads `process.env`; **Expo requires the `EXPO_PUBLIC_` prefix** to expose a variable to app code (`process.env.EXPO_PUBLIC_...`)
- [ ] **🔑 The critical client-app nuance** — anything shipped to the phone (any `EXPO_PUBLIC_` value, including the Supabase **anon/publishable key**) is **embedded in the app bundle and is NOT secret**. The anon key is safe to expose *only because RLS protects the data* — not because it's hidden. **True secrets — the Supabase `service_role` key, any API secret — must stay server-side (Edge Functions) and NEVER ship to the client** (the service key bypasses RLS entirely)
- [ ] **Never commit `.env`** — add it to `.gitignore` (light recall of Git Stage 2); leaked secrets in Git history are a classic breach
### Should-Know Topics 🟡
- [ ] **Secrets in CI/deployment (light recall → point back)** — your build/deploy pipeline also needs these values (e.g. EAS build environment variables, GitHub Actions secrets). You already have the CI-secrets mechanics in **GitHub — Phase 1, Stage 5** (secrets, `GITHUB_TOKEN`, permissions) — refer back there rather than re-learning it here. The new idea in *this* roadmap is only the *client-vs-server secret* distinction above.
### Nice-to-Know Topics 🟢
- [ ] **Secret managers & rotation** — tools like Doppler/Vault and the practice of rotating keys; awareness only
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me environment variables and `.env` files, including Expo's `EXPO_PUBLIC_` convention. Quiz me on why config belongs outside code."
> 2. "Teach me the client-vs-server secret distinction for a client app: why anything with `EXPO_PUBLIC_` is not secret, why the Supabase anon key is safe to expose but the service_role key never is, and why RLS is what actually protects the data. Give me a list of keys and make me classify each as ship-to-client or server-only."

---

## 🏁 Final Milestone
You can explain the full identity story of the Visual Life Archive app: how a user logs in, what proof the client holds and where on the device it's stored, how the app stays logged in, and how the backend guarantees each user sees only their own moments. And you can explain the full configuration story: which values are safe to embed in the shipped app, which must never leave the server and why, and how to keep `.env` out of Git. You can set up a correct `.env` for the app without leaking anything.

---

## ⏭️ What's Out of Scope (For Now)
- **Building your own auth server / password hashing internals** (bcrypt/argon2) — Supabase handles this; you won't reimplement it.
- **Writing RLS policies in depth / authorization systems (RBAC)** — concept only here; policy-writing belongs in the future **Supabase** roadmap.
- **OAuth / social-login deep flow + deep-linking setup** — awareness only; the app-specific wiring lives in the React Native / Supabase build work.
- **Cryptography internals** — how signatures are computed, HS256 vs RS256 math.
- **CI/deployment secrets mechanics** — covered in **GitHub — Phase 1, Stage 5**; only lightly recalled here.
- **Secret-management platforms & key-rotation policy** (Doppler, Vault) — awareness only.
- **Web cookie-security deep-dive** — SameSite, CSRF tokens, the BFF pattern; relevant to the web version later, not to this phase.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Fundamentals: "Teach me authentication vs authorization with clear examples, and the universal login flow — credentials, verification, proof of identity, sending that proof on later requests. Quiz me until I can explain each step and why HTTP being stateless makes it necessary."
2. Stage 2 — Sessions vs tokens: "Teach me session-based vs token-based authentication — stateful server sessions with a session-ID cookie vs stateless signed tokens. Quiz me on the trade-offs."
3. Stage 2 — JWTs: "Teach me what a JWT is — header, payload, signature — and why the payload is readable (never a secret store) while the signature proves integrity. Include access vs refresh tokens. Make me explain each part back."
4. Stage 3 — Supabase Auth: "Teach me how Supabase Auth works in an Expo React Native app — sign up/in/out, the session object, and how it persists login across restarts. Relate each piece to the sessions/tokens concepts. Quiz me on where the token lives."
5. Stage 3 — RLS & secure storage: "Teach me, at a concept level, how Row-Level Security makes it safe to query the database directly from the app so each user only sees their own data, and why the session should live in secure device storage. Make me explain the end-to-end privacy story for my app."
6. Stage 4 — Env vars: "Teach me environment variables and `.env` files, including Expo's `EXPO_PUBLIC_` convention. Quiz me on why config belongs outside code."
7. Stage 4 — Client vs server secrets: "Teach me the client-vs-server secret distinction: why anything with `EXPO_PUBLIC_` is not secret, why the Supabase anon key is safe to expose but the service_role key never is, and why RLS actually protects the data. Give me a list of keys and make me classify each as ship-to-client or server-only."
