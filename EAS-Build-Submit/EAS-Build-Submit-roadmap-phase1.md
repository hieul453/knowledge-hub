# Learning Roadmap: Expo EAS Build & App Store Submission — Phase 1

**Goal:** Take the finished Visual Life Archive app from source code to an installable build and into the app stores — using Expo's cloud build/submit service (EAS) so you never need a Mac. You'll learn how builds, app signing, and store submission actually work, and end able to get your app onto a real device and into TestFlight / Google Play testing.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). This is the *deployment* stage — the last thing you do, after the app is built.
**Time budget:** ~10–14 hrs of focused learning. ⚠️ *Calendar* time is longer: account verification, Google's tester requirement, and store review add days-to-weeks of waiting you don't control.
**Starting point:** You have a working Expo app to build. This roadmap is about shipping it, not writing it.

---

## 🗺️ Overview

**EAS (Expo Application Services)** is Expo's cloud platform for shipping apps. It has three parts: **EAS Build** compiles your iOS and Android binaries in the cloud (no Xcode, no Android Studio, no Mac), **EAS Submit** uploads those binaries to the App Store and Google Play, and **EAS Update** pushes JavaScript changes over-the-air without a new store build. This roadmap walks the real pipeline: understand the build model and profiles, handle **app signing and identity** (the part beginners fear — but EAS manages it for you), run actual builds and get them onto a device, then submit to the stores and understand the review gauntlet. The end state is your app live in TestFlight / Google Play testing, with a clear map of the cost and steps to full public release.

---

## ⚠️ A Note On Starting Point & Money (read this)

Two things make this roadmap different from the others:
1. **You need a working app first.** EAS builds *something* — if the React Native app isn't running locally, there's nothing to ship. Do the React Native + Expo roadmap before the hands-on parts here (you can still learn the *concepts* anytime).
2. **This is where real money appears.** Everything up to now had free tiers. Publishing needs developer accounts: **Apple Developer Program — $99/year (recurring)** and **Google Play Console — $25 one-time**. EAS Build itself has a free tier (limited monthly build minutes) that's fine for learning. You can do almost all of this roadmap — including installing builds on your own devices — before paying anything; the fees are only required to *submit to the stores*.

---

## Prerequisites (Complete Before the Hands-On Stages)

- [ ] **A working Expo / React Native app** 🔴 — from the React Native + Expo roadmap. Needed for Stages 3–4 (the build/submit steps); Stages 1–2 are concept and can be done earlier. — est. *(covered in RN roadmap)*
- [ ] **Environment variables & secrets concept** 🟡 — from your Auth & Secrets roadmap (Stage 4); you'll set build-time env vars and understand which keys are safe. — est. *(covered there)*
- [ ] **Git/GitHub basics** 🟢 — for the optional CI-triggered builds and general project hygiene. — est. *(covered in Git roadmap)*
> ✅ Stages 1–2 need no app and no payment — start them whenever.

---

## Stage 1: EAS & the Build/Submit Mental Model
**Goal of this stage:** Understand what EAS is, why it removes the Mac requirement, and the build-profile system — before running anything.
**Estimated time:** 2–3 hrs
**Milestone:** You can explain what EAS Build, EAS Submit, and EAS Update each do, why no Mac/Xcode is needed, and the three build profiles (development / preview / production) and when each is used.

### Must-Know Topics 🔴
- [ ] **What EAS is** — Expo Application Services: **EAS Build** (cloud native builds), **EAS Submit** (upload to stores), **EAS Update** (over-the-air JS updates)
- [ ] **Why no Mac is needed** — iOS builds run on Expo's hosted **macOS cloud**, Android builds on Linux cloud; this is the thing that unblocks you on Windows
- [ ] **Build profiles & `eas.json`** — the `development` / `preview` / `production` profiles live in `eas.json`; you pick one with `--profile` (production is the default)
- [ ] **The three build types** — *development* (includes dev tools via `expo-dev-client`, never submitted to a store), *preview* (internal testing, direct install), *production* (what goes to stores)
- [ ] **Build artifacts** — **AAB** (Android App Bundle, the store default) vs **APK** (direct install for testing); iOS produces an **IPA**
### Should-Know Topics 🟡
- [ ] **Internal distribution** — sharing a build via URL to install directly on physical devices, before any store is involved
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what Expo EAS is — Build, Submit, and Update — and why EAS Build means I don't need a Mac to build iOS. Quiz me on what each service does."
> 2. "Teach me EAS build profiles (development / preview / production) in eas.json, the three build types, and APK vs AAB. Give me scenarios and make me pick the right profile and artifact."

---

## Stage 2: App Identity, Credentials & Signing
**Goal of this stage:** Understand app signing (the scary-sounding part) and set your app's permanent identity — with EAS doing the hard cryptographic work.
**Estimated time:** 2–3 hrs
**Milestone:** Your app's identity is configured (bundle identifier / package name, name, icon, splash), you understand what signing is and why stores demand it, and you've let EAS manage your credentials.

### Must-Know Topics 🔴
- [ ] **What app signing is & why** — a cryptographic signature proving the app genuinely comes from you; stores require it, and it's what makes secure updates possible
- [ ] **The credentials, per platform** — iOS needs a **distribution certificate + provisioning profile**; Android needs a **release keystore**. **EAS can generate and securely store all of these for you** (the big beginner win) — or you can bring your own
- [ ] **App identifiers** — iOS **`bundleIdentifier`** and Android **package name**, in reverse-domain form (e.g. `com.hieu.visuallifearchive`); these are effectively **permanent once published**, so choose carefully
- [ ] **App presentation & versioning** — app name, icon, splash screen, and the difference between the user-facing **version** and the internal **build number**
- [ ] **The two developer accounts** — **Apple Developer Program ($99/year, recurring)** and **Google Play Console ($25 one-time)**; what each unlocks
### Should-Know Topics 🟡
- [ ] **`app.json` / `app.config.js`** — where the identifiers, icon, splash, and version live in an Expo project
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me app signing for iOS and Android — distribution certificates/provisioning profiles vs the Android keystore — and how EAS manages these credentials so I don't have to. Quiz me on why signing exists."
> 2. "Teach me app identity in an Expo app — bundle identifier / package name (and why they're permanent), version vs build number, icon and splash. Make me define these correctly for my app."

---

## Stage 3: Running EAS Build
**Goal of this stage:** Actually produce installable builds of your app and get them onto a real device.
**Estimated time:** 3–4 hrs
**Milestone:** You've produced a real installable build of the Visual Life Archive app — an Android APK you can sideload and an iOS build via the cloud — and run it on a physical device.

### Must-Know Topics 🔴
- [ ] **Set up EAS** — install EAS CLI (`npm install -g eas-cli`), `eas login`, and `eas build:configure` (which creates/normalizes `eas.json`)
- [ ] **Run a build** — `eas build --platform android|ios|all --profile preview|production`; monitor progress and read logs on the EAS dashboard
- [ ] **Get the build on a device** — internal-distribution APK/ad-hoc install for quick testing; **TestFlight** (iOS) and **Play internal testing** (Android) for store-channel testing
- [ ] **Build-time environment variables** — the `env` field per profile in `eas.json` (and EAS environment variables) so each build gets the right config. *The concept of which keys are safe to embed lives in your Auth & Secrets roadmap (Stage 4); CI-secret mechanics live in GitHub Phase 1 Stage 5 — here it's specifically the EAS `env` wiring.*
### Should-Know Topics 🟡
- [ ] **Development builds** — a build with `expo-dev-client` for testing native modules on-device during development (vs Expo Go)
### Nice-to-Know Topics 🟢
- [ ] **Local builds** — `eas build --local` for building on your own machine (Android on Windows; iOS still needs macOS)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the EAS Build workflow hands-on — installing EAS CLI, `eas login`, `eas build:configure`, and running `eas build` with a profile. Walk me through reading the build dashboard, then quiz me on the commands."
> 2. "Teach me how to get an EAS build onto a physical device — internal distribution vs TestFlight vs Play internal testing — and how to set build-time env vars via the `env` field in eas.json. Make me explain when I'd use each distribution method."

---

## Stage 4: Store Submission & Review
**Goal of this stage:** Submit the app to the stores with EAS Submit and understand the review gauntlet standing between you and a public release.
**Estimated time:** 3–4 hrs
**Milestone:** You've submitted the app end to end to at least one store's internal/testing track, and you know the exact remaining steps, costs, and gotchas to reach public production.

### Must-Know Topics 🔴
- [ ] **EAS Submit** — `eas submit --platform ...`, the `--auto-submit` flag to chain build → submit, and **submit profiles** in `eas.json`
- [ ] **The iOS path** — EAS uploads to **App Store Connect**, where the build lands in **TestFlight** (internal testing) after processing; reaching the public App Store requires you to **manually complete the store listing** (metadata, screenshots, **privacy "nutrition" labels**) and **submit for App Review** in App Store Connect
- [ ] **The Android path** — via **Google Play Console**; the **very first submission must be uploaded manually** (a Play API limitation), then release **tracks** progress internal → closed → open → production; you must complete the **Data safety form**, content rating, and store listing
- [ ] **⚠️ Real-world gotchas** — Google **personal accounts require closed testing with 12 testers for 14 days** before production; both stores require a **privacy policy** (your app stores photos + account data, so this applies); build **review timelines** and common **rejection reasons** (broken functionality, missing privacy policy, incomplete metadata)
### Should-Know Topics 🟡
- [ ] **EAS Update (OTA)** — push JS/asset fixes without a new build or store review, via update **channels** mapped to build profiles, with **staged rollout %**; know that **native changes still require a full new build** (OTA can't ship those)
- [ ] **Versioning for releases** — remote version management / auto-incrementing build numbers so each submission is unique
### Nice-to-Know Topics 🟢
- [ ] **CI-triggered build + submit** — EAS Workflows / GitHub Actions to build and submit on push to `main` (the CI *concepts* are in GitHub Phase 1 Stage 5)
- [ ] **EAS pricing tiers & build minutes** — what the free tier gives you and when you'd pay
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me EAS Submit — `eas submit`, `--auto-submit`, and submit profiles — and the full iOS path (App Store Connect → TestFlight → App Review) and Android path (Play Console, manual first upload, release tracks, Data safety form). Quiz me on the sequence for each platform."
> 2. "Teach me the real-world app store gotchas — Google's 12-tester/14-day rule, privacy policy requirements, review timelines, and common rejection reasons — plus what EAS Update (OTA) can and cannot ship. Make me lay out the remaining steps from testing track to public production for my app."

---

## 🏁 Final Milestone
You can take the finished Visual Life Archive app from source to an installable build via **EAS Build** with no Mac, install it on your own device, and push it through **EAS Submit** to TestFlight / Google Play internal testing. You understand app signing (and why EAS handling it is a gift), your app's permanent identity, every cost involved, and the full review path — including the 12-tester rule, privacy-policy requirement, and manual-first-submission quirk — needed to reach a public production release. You also know how EAS Update lets you ship JS fixes without waiting on store review.

---

## ⏭️ What's Out of Scope (For Now)
- **Building the app / React Native feature code** — that's the React Native + Expo roadmap; this one assumes a working app.
- **Web deployment (Vercel)** for the web version — a different pipeline; separate concern.
- **Deep CI/CD pipeline authoring** — CI mechanics live in **GitHub Phase 1, Stage 5**; only a nice-to-know cross-reference here.
- **Manual native credential management & Fastlane** — EAS replaces these; only "bring-your-own credentials" is mentioned.
- **Custom native modules / bare-workflow prebuild deep-dive.**
- **App Store Optimization (ASO), marketing, monetization, in-app purchases & commission optimization** — business concerns beyond getting the app published.
- **EU DMA / alternative app stores, enterprise & MDM distribution.**

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — EAS overview: "Teach me what Expo EAS is — Build, Submit, and Update — and why EAS Build means I don't need a Mac to build iOS. Quiz me on what each service does."
2. Stage 1 — Profiles: "Teach me EAS build profiles (development / preview / production) in eas.json, the three build types, and APK vs AAB. Give me scenarios and make me pick the right profile and artifact."
3. Stage 2 — Signing: "Teach me app signing for iOS and Android — distribution certificates/provisioning profiles vs the Android keystore — and how EAS manages these credentials. Quiz me on why signing exists."
4. Stage 2 — Identity: "Teach me app identity in an Expo app — bundle identifier / package name (and why they're permanent), version vs build number, icon and splash. Make me define these for my app."
5. Stage 3 — Build workflow: "Teach me the EAS Build workflow hands-on — EAS CLI, `eas login`, `eas build:configure`, and running `eas build` with a profile. Walk me through the build dashboard, then quiz me on the commands."
6. Stage 3 — Distribution & env: "Teach me getting an EAS build onto a device — internal distribution vs TestFlight vs Play internal testing — and setting build-time env vars via the `env` field in eas.json. Make me explain when to use each distribution method."
7. Stage 4 — Submit: "Teach me EAS Submit — `eas submit`, `--auto-submit`, submit profiles — and the full iOS path (App Store Connect → TestFlight → App Review) and Android path (Play Console, manual first upload, tracks, Data safety form). Quiz me on the sequence."
8. Stage 4 — Gotchas & OTA: "Teach me the real app store gotchas — Google's 12-tester/14-day rule, privacy-policy requirements, review timelines, common rejections — and what EAS Update can and cannot ship. Make me lay out the steps from testing track to public production."
