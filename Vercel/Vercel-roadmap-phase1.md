# Learning Roadmap: Vercel — Deploying the Web Version — Phase 1

**Goal:** Deploy the web version of the Visual Life Archive app to a live, public URL on Vercel — and understand the deployment model well enough to ship confidently: push-to-deploy from Git, preview vs production, environment variables, custom domains, and rollbacks. Vercel skills transfer to almost any modern web project, so this is broadly useful beyond this app.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). This is the *web-deployment* counterpart to the EAS roadmap (which ships the mobile apps). Your Expo project produces a web build; Vercel hosts it.
**Time budget:** ~6–10 hrs. Vercel is one of the more beginner-friendly pieces of your stack.
**Starting point:** You have (or will have) a web build of the app — Expo's web export. This roadmap is about hosting it, not building it.

---

## 🗺️ Overview

Vercel is a hosting platform built around one idea: **connect a Git repository, and every push builds and deploys automatically**, with HTTPS and a global CDN handled for you. The mental model to internalize is the split between **preview** deployments (every branch/PR gets its own URL to test on) and **production** (your main branch, served on your real domain). This roadmap starts with that model, then gets your Expo web build actually deployed, then layers on the real-world essentials — environment variables (so the deployed site can reach Supabase), custom domains, and the push→preview→production→rollback workflow. Because your backend is Supabase, you're deploying a static single-page app, which is the simplest and cleanest case Vercel handles.

---

## ⚠️ A Note On What "The Web Version" Is (read this)

Your app is built with Expo/React Native. The **web version** is that same app rendered in a browser via **React Native for Web**, produced by Expo's web export (`expo export -p web`, which outputs a `dist` folder). So "deploying the web version" means: build the Expo web export, and have Vercel serve that `dist` output. You don't write a separate website — it's the same codebase, exported for web. You can learn Vercel's fundamentals by deploying *any* simple site first, then apply them to the Expo export.

---

## Prerequisites (Complete Before the Hands-On Stages)

- [ ] **A Git repository on GitHub** 🔴 — Vercel deploys *from* Git; this is the heart of the workflow. From your Git/GitHub roadmaps. — est. *(covered there)*
- [ ] **A web build of the app (Expo web export) — or any static site to practice on** 🔴 — needed for Stages 2–4. You can practice Stage 1–2 mechanics with a trivial site before the real app is ready. — est. *(app comes from the RN roadmap)*
- [ ] **Environment variables & secrets concept** 🟡 — from your Auth & Secrets roadmap (Stage 4); you'll set Supabase keys in Vercel and the same client-vs-server rule applies. — est. *(covered there)*
> ✅ Stage 1 is pure concept. The free **Hobby** tier covers everything in this roadmap at $0.

---

## Stage 1: What Vercel Is & the Deployment Mental Model
**Goal of this stage:** Understand how Vercel deploys apps and the preview-vs-production model — before deploying anything.
**Estimated time:** 1–2 hrs
**Milestone:** You can explain the connect-repo → build → deploy flow, and the difference between a **preview** deployment and a **production** deployment.

### Must-Know Topics 🔴
- [ ] **What Vercel is** — a hosting/deployment platform for frontend/web apps; you connect a Git repo and it builds + serves your site, with automatic **HTTPS** and a global **CDN**
- [ ] **Push-to-deploy** — the core workflow: every commit/PR to the connected repo triggers a new deployment automatically
- [ ] **Preview vs production** — the production branch (usually `main`) serves your real domain; **every other branch/PR gets its own preview URL** to test on before going live. This is the single most important Vercel concept.
- [ ] **Build vs output** — the **build command** (e.g. `expo export -p web`) and the **output directory** (e.g. `dist`) that Vercel serves; framework detection vs manual config
### Should-Know Topics 🟡
- [ ] **The three environments** — Local (your machine), Preview, Production — and that they can have different environment variables
- [ ] **The Hobby (free) tier** — what personal projects get at no cost
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what Vercel is and its deployment model — connect a Git repo, push-to-deploy, automatic HTTPS/CDN, and especially preview vs production deployments. Quiz me until I can explain what happens when I push to a feature branch vs to main."

---

## Stage 2: Deploying the App's Web Version
**Goal of this stage:** Get the Expo web build live on a Vercel URL.
**Estimated time:** 2–3 hrs
**Milestone:** The Visual Life Archive web version is deployed to a live `*.vercel.app` URL from your GitHub repo.

### Must-Know Topics 🔴
- [ ] **The Expo web export** — `expo export -p web` produces a `dist` folder (a static single-page app rendered via React Native for Web)
- [ ] **Connecting the repo** — importing your GitHub project in Vercel ("New Project"), which sets up automatic deployments
- [ ] **Build settings** — configuring the **build command** (`expo export -p web`) and **output directory** (`dist`); setting **framework preset** to none/other for an Expo SPA
- [ ] **`vercel.json` for SPA routing** — adding rewrites so all routes serve the app (client-side routing), e.g. rewriting `/:path*` → `/`, plus `cleanUrls` and `framework: null`
### Should-Know Topics 🟡
- [ ] **The generated URL** — the automatic `*.vercel.app` domain your deploy gets, and the per-branch preview URLs
### Nice-to-Know Topics 🟢
- [ ] **Vercel Drop / CLI deploy** — deploying a folder by drag-and-drop or `vercel` from the terminal, without Git (handy for a quick test)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me how to deploy an Expo web export to Vercel — the `expo export -p web` build command, the `dist` output directory, and importing the GitHub repo. Quiz me on the build settings."
> 2. "Teach me `vercel.json` for a single-page app — why SPA rewrites are needed so client-side routes work, plus `cleanUrls` and `framework: null`. Make me explain what breaks without the rewrite."

---

## Stage 3: Environment Variables, Domains & Configuration
**Goal of this stage:** Make the deployed app reach Supabase and (optionally) run on your own domain.
**Estimated time:** 2–3 hrs
**Milestone:** Your deployed app reads its Supabase config from Vercel environment variables, and you understand how to attach a custom domain with HTTPS.

### Must-Know Topics 🔴
- [ ] **Environment variables in Vercel** — adding variables in the dashboard, and that they're scoped **per environment** (production / preview / development); changes apply only to *new* deployments
- [ ] **The client-vs-server rule still applies** — anything the browser bundle needs (your Supabase URL + anon/publishable key) is exposed to the client; that's fine *because RLS protects the data* — but the `service_role` key must **never** be set as a client-exposed variable. (This is the same rule from your Auth & Secrets roadmap, Stage 4 — applied to Vercel.)
- [ ] **Custom domains** — adding a domain to a project, pointing DNS, and Vercel's **automatic HTTPS/SSL**
### Should-Know Topics 🟡
- [ ] **Per-environment values** — using different Supabase projects/keys for preview vs production so testing never touches production data
- [ ] **Build configuration** — Node version, output settings, and where to change them
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me environment variables in Vercel — how they're scoped per environment, how to set my Supabase URL and anon key, and why the service_role key must never be exposed to the client. Quiz me on which keys are safe to add."
> 2. "Teach me custom domains on Vercel — adding a domain, DNS pointing, and automatic HTTPS. Make me explain the steps to put my app on a real domain."

---

## Stage 4: The Deployment Workflow & Operations
**Goal of this stage:** Run the full real-world loop and know how to recover when a deploy goes wrong.
**Estimated time:** 1–2 hrs
**Milestone:** You can run the full cycle — push a branch → get a preview URL → merge to main → production deploy — and instantly roll back a bad production deploy.

### Must-Know Topics 🔴
- [ ] **The Git-driven loop** — push to a feature branch → automatic **preview** deployment with its own URL → merge to `main` → automatic **production** deployment
- [ ] **Preview deployments for review** — testing/QA on the preview URL *before* it reaches production
- [ ] **Instant rollback** — reverting production to a previous deployment by re-pointing domains (no rebuild); on Hobby you can roll back to the immediately previous deployment
- [ ] **Build logs & troubleshooting** — reading logs to diagnose a failed build
### Should-Know Topics 🟡
- [ ] **Vercel CLI** — `vercel` (deploy), `vercel --prod`, `vercel rollback`, `vercel promote` for terminal-driven workflows
- [ ] **Vercel vs GitHub Actions** — Vercel auto-deploys on push (its *own* pipeline); this **complements** rather than replaces GitHub Actions CI (from GitHub Stage 5) — you can run your test suite in Actions and let Vercel handle the deploy
### Nice-to-Know Topics 🟢
- [ ] **Web Analytics / Speed Insights** — built-in performance/traffic monitoring (awareness)
- [ ] **Deploy hooks** — triggering a deploy via a URL without a commit
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the Vercel Git deployment workflow end to end — feature branch → preview URL → merge to main → production — and instant rollback. Quiz me on how I'd recover from a broken production deploy."
> 2. "Teach me how Vercel's push-to-deploy relates to GitHub Actions CI — what each is responsible for and how they work together (tests in Actions, deploy on Vercel). Make me explain the division of labor."

---

## 🏁 Final Milestone
You can take the Visual Life Archive web export and deploy it to a live Vercel URL from GitHub, wire it to Supabase through environment variables (without exposing anything you shouldn't), optionally serve it on a custom domain with HTTPS, and operate it day to day: push → preview → production, with instant rollback when something breaks. You understand how this web pipeline sits alongside — not on top of — your GitHub Actions CI and your EAS mobile deployment.

---

## ⏭️ What's Out of Scope (For Now)
- **Building the web app itself** — the Expo web output comes from the React Native + Expo roadmap; this one only hosts it.
- **Vercel Functions / Edge Functions / API routes** — server-side compute on Vercel. Your backend is **Supabase**, so you don't need these; awareness only.
- **Next.js-specific features** (SSR/ISR/App Router/Server Components) — Vercel is Next.js's home, but your app isn't Next.js. Out of scope; revisit only if you ever adopt Next.
- **Mobile app deployment** — that's the **EAS Build & Submit** roadmap.
- **CI test pipelines** — live in **GitHub Phase 1, Stage 5**; only cross-referenced here.
- **DNS deep-dive, advanced CDN/caching tuning, monorepo configuration, team/Enterprise features, custom environments** — beyond a single personal web deploy.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Model: "Teach me what Vercel is and its deployment model — connect a Git repo, push-to-deploy, automatic HTTPS/CDN, and especially preview vs production. Quiz me until I can explain what happens when I push to a feature branch vs to main."
2. Stage 2 — Deploy: "Teach me how to deploy an Expo web export to Vercel — the `expo export -p web` build command, the `dist` output directory, and importing the GitHub repo. Quiz me on the build settings."
3. Stage 2 — SPA config: "Teach me `vercel.json` for a single-page app — why SPA rewrites are needed so client-side routes work, plus `cleanUrls` and `framework: null`. Make me explain what breaks without the rewrite."
4. Stage 3 — Env vars: "Teach me environment variables in Vercel — per-environment scoping, setting my Supabase URL and anon key, and why the service_role key must never be exposed. Quiz me on which keys are safe."
5. Stage 3 — Domains: "Teach me custom domains on Vercel — adding a domain, DNS pointing, and automatic HTTPS. Make me explain the steps."
6. Stage 4 — Workflow: "Teach me the Vercel Git workflow end to end — feature branch → preview URL → merge to main → production — and instant rollback. Quiz me on recovering from a broken production deploy."
7. Stage 4 — Vercel vs CI: "Teach me how Vercel's push-to-deploy relates to GitHub Actions CI — what each does and how they work together. Make me explain the division of labor."
