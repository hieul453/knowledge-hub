# Learning Roadmap: React Native + Expo — Phase 1

**Goal:** Build the **Visual Life Archive** app — a real mobile app where a logged-in user captures/picks photos, adds a caption and date, and browses them in a grid — with **auth + photo storage + data all on Supabase**. Not RN mastery; the foundational concepts + the exact stack your app needs, understood *why*-first.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). This is the "own separate roadmap" your React (core concepts) Phase 1 plan pointed to as its next step.
**Time budget:** ~**50–65 hrs** of focused study + practice for React Native + Expo itself — **on top of** the React (core concepts) Phase 1 roadmap (~20–30 hrs), which is a hard prerequisite here. Flexible pace; tell me your weekly hours and I'll convert to a calendar.
**Starting point:** Total beginner to mobile. You have *not* started React (core concepts) Phase 1 yet — so that comes first (see Prerequisites). This roadmap is written in **JavaScript**, not TypeScript (see the note below).

---

## 🗺️ Overview

React Native lets you build a **real native mobile app using React** — the same components, props, `useState`, `useEffect`, and one-way data flow you learn in React, except the building blocks render to actual native UI (`<View>` instead of `<div>`, `<Text>` instead of `<span>`) instead of a webpage. **Expo** is the framework and tooling layer on top that removes the native-build pain: you scaffold in one command, run on your real phone in seconds via Expo Go, and reach the camera, image picker, and secure storage through ready-made modules. This roadmap starts from that mental model, builds the UI skills (core components, styling with Flexbox, lists, file-based navigation), adds the device capabilities your app needs (camera/photos/permissions), then brings in **Supabase** as the backend (auth, a Postgres database, and file storage) — and finishes by assembling the whole Visual Life Archive loop end to end on your phone.

---

## ⚠️ A Note On Your Starting Point (read this)

**React Native *is* React.** Everything that makes React confusing to a beginner — why changing state re-renders, why props are read-only, why `.map()` renders a list, why `useEffect` runs when it does — is *identical* in React Native. RN only swaps the building blocks and adds mobile concerns (native components, Flexbox-by-default, device permissions). If you try to learn React Native before React clicks, you'll be learning two hard things at once and blaming React Native for the pain — exactly the warning your React roadmap opens with. **So do React (core concepts) Phase 1 first.** It's not optional; it's the foundation this entire roadmap stands on.

**On JavaScript vs TypeScript:** this roadmap is written in **JavaScript**, matching your established pattern (learn the concept first, add types as a layer later — the way your JS and React roadmaps both defer TypeScript). One wrinkle: `create-expo-app` scaffolds a **TypeScript** template by default now. Two clean ways to handle it: (a) accept the TS template but write your files as plain `.js`/`.jsx` and don't annotate types yet, or (b) rename files to `.js` as you go. Either is fine. When you're ready to add types, your **TypeScript Phase 1** roadmap is where that happens — and RN + Expo are TypeScript-native, so it retrofits cleanly.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **React (core concepts) Phase 1** 🔴 — *the* prerequisite. Components, JSX, props + one-way flow, list rendering with `key`, `useState` + the render loop, controlled inputs, `useEffect` + data fetching, and lifting state up. RN reuses every one of these unchanged. — est. **~20–30 hrs (your React roadmap)**
- [ ] **JavaScript Phase 1, Stages 1–3** 🔴 — variables/functions/objects/arrays, `map`/`filter`, and especially **`async`/`await`** (Supabase calls and image uploads are all async). Already a prereq of your React roadmap. — est. *(covered by your JS roadmap)*
- [ ] **Node.js + npm** 🟡 — installing packages, `package.json`, running npm scripts. Expo installs and runs via Node. — est. **0–1 hr (you have this)**
- [ ] **A phone with the Expo Go app** (iOS or Android) 🔴 — the fastest way to see your app on a real device; an emulator/simulator works too but a physical phone is the smoothest start. — est. **15 min**
- [ ] **A free Supabase account** 🟡 — you'll create the project in Stage 5, but signing up now removes a gate later. — est. **15 min**
> ✅ Skip any you already have. **Do not skip React (core concepts) Phase 1** — if React hasn't clicked, RN won't either.

---

## Stage 1: What React Native + Expo Are — Mental Model & First Screen
**Goal of this stage:** Understand *why* RN is "React that renders native," what Expo adds on top, and get an app running on your own phone.
**Estimated time:** 4–6 hrs
**Milestone:** You can scaffold an Expo app, run it on your phone via Expo Go with live reload, render a first screen using `<View>`/`<Text>`/`<Image>`, and explain — in plain language — how React Native differs from React-for-the-web and what problem Expo solves.

### Must-Know Topics 🔴
- [ ] **React Native's model** — your JS/React renders to *real native components*, not a webview; "learn React once, apply it on mobile." This single fact explains why your React knowledge transfers wholesale.
- [ ] **What Expo is** — a framework + tooling layer over RN: one-command scaffolding, Expo Go for instant on-device runs, and prebuilt native modules (camera, storage) so you rarely touch Xcode/Android Studio.
- [ ] **`create-expo-app` + project structure** — scaffolding a project, the `app/` directory, running `npx expo start`, scanning the QR code into Expo Go, Fast Refresh.
- [ ] **Core components vs the web** — `<View>` (≈ `div`), `<Text>` (all text must live in `<Text>`), `<Image>`, `<ScrollView>`; how JSX/props/state you already know apply here unchanged.
### Should-Know Topics 🟡
- [ ] **The New Architecture** — in current Expo SDKs it's always on and automatic; you don't configure it, but know the term exists so docs make sense.
- [ ] **Managed workflow & EAS (awareness only)** — that Expo can later build store binaries for you; you won't need it this phase.
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what React Native is and how it relates to React — that it renders real native components, and that my React knowledge (components, props, state, effects) transfers unchanged. Then teach me what Expo adds on top. Quiz me until I can explain *why* RN is 'React for mobile' and what Expo solves."
> 2. "Walk me through scaffolding an Expo app with `create-expo-app`, running it on my phone via Expo Go, and the core components `View`/`Text`/`Image`/`ScrollView` vs their web equivalents. Make sure I can explain the project structure and why all text must sit inside `<Text>`."

---

## Stage 2: Building UIs — Core Components, Styling & Flexbox
**Goal of this stage:** Lay out and style a real mobile screen using RN's styling system and Flexbox, and wire up interaction.
**Estimated time:** 6–8 hrs
**Milestone:** You can build a styled, static **DayCard** component (photo + caption + date) using `StyleSheet.create` and Flexbox, arrange several down the screen, handle a tap, and take text input — and explain how RN styling differs from CSS.

### Must-Know Topics 🔴
- [ ] **Styling in RN** — `StyleSheet.create`, style objects instead of CSS files, **camelCase** props (`backgroundColor`), density-independent pixel units, no cascade/inheritance the way web CSS has.
- [ ] **Flexbox in React Native** — the primary layout tool; **`flexDirection` defaults to `column`** (unlike web), `flex`, `justifyContent`, `alignItems`; every `<View>` is a flex container.
- [ ] **Interaction & input** — `Pressable` (and `TouchableOpacity`), `Button`, and **`TextInput`** as a controlled input (ties straight to your React controlled-forms skill).
- [ ] **Safe areas** — `SafeAreaView` / `react-native-safe-area-context` so content doesn't collide with notches/status bars.
### Should-Know Topics 🟡
- [ ] **Platform differences** — `Platform.OS`, small iOS/Android styling divergences, and why you test on both.
- [ ] **`@expo/vector-icons`** — ready-to-use icon sets for buttons and tabs (bundled with Expo).
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me styling in React Native — `StyleSheet.create`, style objects, camelCase, dp units — and how it differs from web CSS. Then teach me Flexbox in RN, emphasizing that `flexDirection` defaults to `column`. Give me layouts to build and quiz me on the flex properties."
> 2. "Teach me the interactive core components — `Pressable`/`TouchableOpacity`, `Button`, and `TextInput` as a controlled input — plus safe areas. Make me wire up a tappable, styled card with a text field."

---

## Stage 3: Lists & Navigation — FlatList + Expo Router
**Goal of this stage:** Render a scrollable photo grid efficiently and move between screens with file-based routing.
**Estimated time:** 8–11 hrs
**Milestone:** You can build a **photo-grid screen** with `FlatList` (`numColumns`, `renderItem`, `keyExtractor`) and make tapping an item navigate to a detail screen using **Expo Router** — and explain why `FlatList` beats `ScrollView` for long lists.

### Must-Know Topics 🔴
- [ ] **`FlatList`** — the virtualized list component: `data`, `renderItem`, `keyExtractor`, and **`numColumns`** for a grid; why it only renders visible rows (vs `ScrollView` rendering everything). Your React "render a list with keys" skill, made performant for mobile.
- [ ] **`ScrollView` vs `FlatList`** — when each is right; the memory/perf reason to reach for `FlatList` on dynamic/large data.
- [ ] **Expo Router — file-based routing** — the `app/` directory *is* your navigation; files become routes, `_layout` files define shells, `Stack` and `Tabs` navigators, `Link` and `router.push()`.
- [ ] **Dynamic routes & params** — `[id].jsx` routes and reading params, so a grid item can open its own detail screen.
### Should-Know Topics 🟡
- [ ] **FlashList (Shopify)** — the modern drop-in for very large lists; know it exists and why teams pick it over `FlatList` for big datasets.
- [ ] **Tab + stack nesting** — a bottom-tab layout with a stack inside a tab (the shape most real apps take).
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `FlatList` in React Native — `data`/`renderItem`/`keyExtractor`/`numColumns` for a grid — and why it's more efficient than `ScrollView` for long lists. Give me an array of photo objects and make me render a grid; quiz me on when to use which list component."
> 2. "Teach me Expo Router — file-based routing, the `app/` directory, `_layout`, Stack vs Tabs, `Link`/`router.push`, and dynamic `[id]` routes with params. Make me wire a grid screen that navigates to a per-item detail screen."

---

## Stage 4: Native Capabilities — Permissions, Camera & Photos
**Goal of this stage:** Reach the device — pick or capture a photo with permissions handled — which is the raw material of your app.
**Estimated time:** 6–8 hrs
**Milestone:** You can request permission, pick an image from the library **or** capture one with the camera via `expo-image-picker`, and display it — and you understand the local-file-URI you get back (which you'll upload in Stage 5).

### Must-Know Topics 🔴
- [ ] **The Expo SDK module model** — `expo-*` packages, installing with `npx expo install`, and config plugins; how Expo exposes native features without native code.
- [ ] **Permissions** — requesting camera / media-library access, handling grant/deny, and why permission UX matters on mobile.
- [ ] **`expo-image-picker`** — `launchImageLibraryAsync` and `launchCameraAsync`, `allowsEditing`/`aspect`, and the returned **asset URI** (a local `file://` reference, not the image bytes yet).
- [ ] **Displaying local images** — rendering the picked URI with `<Image>` / `expo-image`.
### Should-Know Topics 🟡
- [ ] **Local persistence intro** — `AsyncStorage` vs **`expo-secure-store`** (Keychain/Keystore); a light touch now because Supabase uses one of these to persist your login session in Stage 5.
- [ ] **`expo-image` caching** — faster, cached image rendering for a smooth grid.
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the Expo module + permissions model and `expo-image-picker` — picking from the library and capturing with the camera, handling permissions, and what the returned asset URI actually is. Make me build a 'pick or take a photo and show it' screen."
> 2. "Teach me local persistence on device — `AsyncStorage` vs `expo-secure-store` and when each fits — as groundwork for storing a login session. Quiz me on which to use for sensitive vs non-sensitive data."

---

## Stage 5: The Backend — Supabase Auth, Database & Storage 🧠
**Goal of this stage:** Stand up the whole backend with zero servers: sign users in, store their data in Postgres, and upload their photos to storage — all from the app. This is the biggest new area; slow down.
**Estimated time:** 12–16 hrs
**Milestone:** From the app you can sign a user up/in with a persisted session, `insert`/`select` rows in a table protected by RLS, and upload a photo (from the Stage-4 URI) to a Storage bucket and read it back via its URL.

### Must-Know Topics 🔴
- [ ] **What Supabase is** — a backend-as-a-service: a **Postgres** database with an auto-generated REST API, **Auth**, **Storage**, and **Row Level Security (RLS)** — no server code needed.
- [ ] **`supabase-js` client in Expo** — creating the client, the **storage adapter** (`AsyncStorage`/`SecureStore`) so the session persists, and `EXPO_PUBLIC_*` **environment variables** for URL + publishable/anon key.
- [ ] **Auth** — email/password sign-up and sign-in, `getSession`/`onAuthStateChange`, session persistence, and sign-out.
- [ ] **Database** — modeling a table (e.g. `entries`: user_id, image_path, caption, date), and `select`/`insert`/`update`/`delete` with `supabase.from(...)`.
- [ ] **Row Level Security** — policies that scope rows to `auth.uid()`; **why the anon/publishable key is safe to ship** in a client app because RLS guards the data.
- [ ] **Storage** — buckets, `upload()` from a device file URI, and getting a public or signed URL to render the image in your grid.
### Should-Know Topics 🟡
- [ ] **Session encryption** — the `SecureStore` + `aes-js` pattern Supabase documents for encrypting a stored session (awareness; use the documented recipe).
- [ ] **Reading vs writing the file body** — turning the picker's local URI into uploadable data (the common RN upload gotcha).
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me Supabase as a backend-as-a-service — Postgres + auto REST API + Auth + Storage + Row Level Security — and setting up the `supabase-js` client in an Expo app with a persistent-session storage adapter and `EXPO_PUBLIC_` env vars. Quiz me on *why* shipping the anon key is safe when RLS is on."
> 2. "Teach me Supabase Auth (email/password, session persistence, auth state) and database queries with `supabase.from`, including writing an RLS policy scoped to `auth.uid()`. Make me design the `entries` table and its policies for a per-user photo journal."
> 3. "Teach me Supabase Storage from an Expo app — buckets, uploading a photo from the image-picker's local URI, and getting a URL to display it. Walk me through the URI-to-upload step and quiz me on the common upload pitfalls."

---

## Stage 6: Assembling the App — Auth-Gated Navigation & the Full Loop
**Goal of this stage:** Wire everything into the working Visual Life Archive: protected routes, the capture→upload→save→display loop, and real loading/error/empty states.
**Estimated time:** 10–14 hrs
**Milestone:** The full app works on your phone: a logged-in user captures/picks a photo, adds a caption + date, it uploads to Storage and its metadata saves to the database, and it appears in their grid — **persisting across app restarts and gated behind login**.

### Must-Know Topics 🔴
- [ ] **Auth context + protected routes** — a session provider (your React `useContext`/lifting-state skills) plus **Expo Router**'s `_layout` gate that redirects unauthenticated users to a sign-in screen and signed-in users into the app.
- [ ] **The end-to-end data loop** — capture (Stage 4) → upload to Storage (Stage 5) → write caption/date/image-path to the DB (Stage 5) → fetch and render the grid from the DB (Stage 3).
- [ ] **Loading / error / empty states** — applied to real network + upload calls that take time and can fail (direct recall of React Stage 4); a spinner while uploading, an error on failure, an empty-state when the archive is new.
- [ ] **Data fetching in RN** — `useEffect` + state to load a user's entries on mount and refresh after an insert; when a fixed `useEffect` fetch is enough and when you'd reach for a data library later.
### Should-Know Topics 🟡
- [ ] **App config & assets** — `app.json`, app icon, and splash screen so it feels like a real app.
- [ ] **Pull-to-refresh & optimistic UI** — `FlatList`'s `onRefresh`/`refreshing`, and updating the UI before the server confirms for snappy feel.
- [ ] **`.env` handling & secrets hygiene** — `EXPO_PUBLIC_` vs truly-secret values, and keeping `.env` out of git.
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me auth-gated navigation in Expo Router — a session context/provider plus a `_layout` that redirects based on auth state — reusing my React context and lifting-state knowledge. Make me wire protected routes so unauthenticated users only see sign-in."
> 2. "Walk me through assembling the full Visual Life Archive loop — capture → upload to Supabase Storage → save metadata to the DB → render the grid from the DB — with proper loading/error/empty states. Have me design the data flow end to end and critique it."

---

## 🏁 Final Milestone
You can build a real, useful mobile app from scratch with Expo: a logged-in user captures or picks photos, tags them with a caption and date, and browses them in a grid — with **authentication, a Postgres database, and photo storage all on Supabase, protected by Row Level Security**, running on your actual phone and persisting across restarts. And — the "understand it" part — you can explain to another engineer *why* React Native is "React that renders native," *why* Expo's module model lets you skip native builds, *why* `FlatList` is virtualized, and *why* shipping Supabase's anon key is safe under RLS. At that point you're ready to add TypeScript (your TS roadmap), animations/gestures, and store deployment as clearly-scoped next steps.

---

## ⏭️ What's Out of Scope (For Now)
- **TypeScript with React Native** — the natural next layer; RN + Expo are TS-native and your app retrofits cleanly. Owned by your **TypeScript Phase 1** roadmap — do it *after* the concepts and app are solid, not alongside.
- **Shipping to the App Store / Google Play (EAS Build & Submit)** — you chose "working full app," not "store-shipped." Store deployment (signing, EAS Build, store review) is its own focused mini-roadmap; a strong "next" once the app works.
- **Testing the RN app (Detox, Maestro, React Native Testing Library)** — given your QAOps direction this is a compelling **Phase 2**, and it connects to your JavaScript/Cypress testing tracks. Deliberately excluded here to keep the focus on *building* the app first; you can't meaningfully test an app you haven't built.
- **Animations & gestures (Reanimated, Gesture Handler)** — polish, not foundation; revisit once the core app works.
- **Push notifications, deep linking, and social/OAuth login** — email/password auth covers your app; these are add-ons for later.
- **Realtime & offline sync (Supabase Realtime, local-first)** — powerful, but not needed for the core archive loop.
- **State-management libraries (Redux, Zustand) & data libraries (TanStack Query)** — `useState`/`useContext` + `useEffect` fetching are plenty at this scale; add them the day you feel the pain, not before.
- **Bare/native workflow, custom native modules, the web target** — Expo's managed workflow covers everything here; only leave it if a specific native need forces you to.
- **React Navigation (the standalone library)** — you're learning **Expo Router** (the default in current SDKs) instead; they share concepts, so you can pick up React Navigation later if a project uses it.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order. (Do React (core concepts) Phase 1 first — its own session list.)
1. Stage 1 — RN model: "Teach me what React Native is and how it relates to React — real native components, and that my React knowledge transfers unchanged — then what Expo adds on top. Quiz me until I can explain why RN is 'React for mobile' and what Expo solves."
2. Stage 1 — First app: "Walk me through scaffolding an Expo app with `create-expo-app`, running it on my phone via Expo Go, and core components `View`/`Text`/`Image`/`ScrollView` vs the web. Make sure I can explain the project structure and why all text sits inside `<Text>`."
3. Stage 2 — Styling & Flexbox: "Teach me RN styling — `StyleSheet.create`, style objects, camelCase, dp units — vs web CSS, then Flexbox in RN emphasizing `flexDirection` defaults to `column`. Give me layouts to build and quiz me on flex properties."
4. Stage 2 — Interaction: "Teach me the interactive core components — `Pressable`/`TouchableOpacity`, `Button`, `TextInput` as a controlled input — plus safe areas. Make me wire a tappable, styled card with a text field."
5. Stage 3 — Lists: "Teach me `FlatList` — `data`/`renderItem`/`keyExtractor`/`numColumns` for a grid — and why it beats `ScrollView` for long lists. Give me photo objects to render as a grid; quiz me on when to use which list."
6. Stage 3 — Expo Router: "Teach me Expo Router — file-based routing, `app/` directory, `_layout`, Stack vs Tabs, `Link`/`router.push`, dynamic `[id]` routes with params. Make me wire a grid that navigates to a per-item detail screen."
7. Stage 4 — Camera/photos: "Teach me the Expo module + permissions model and `expo-image-picker` — library pick and camera capture, permissions, and what the returned asset URI is. Make me build a 'pick or take a photo and show it' screen."
8. Stage 4 — Local storage: "Teach me `AsyncStorage` vs `expo-secure-store` and when each fits, as groundwork for storing a login session. Quiz me on sensitive vs non-sensitive data."
9. Stage 5 — Supabase setup: "Teach me Supabase as a BaaS — Postgres + REST + Auth + Storage + RLS — and setting up `supabase-js` in Expo with a persistent-session storage adapter and `EXPO_PUBLIC_` env vars. Quiz me on why shipping the anon key is safe under RLS."
10. Stage 5 — Auth + DB: "Teach me Supabase Auth (email/password, session persistence, auth state) and DB queries with `supabase.from`, including an RLS policy scoped to `auth.uid()`. Make me design the `entries` table and its policies for a per-user photo journal."
11. Stage 5 — Storage: "Teach me Supabase Storage from Expo — buckets, uploading a photo from the image-picker URI, and getting a URL to display it. Walk me through the URI-to-upload step and quiz me on upload pitfalls."
12. Stage 6 — Auth-gated routing: "Teach me auth-gated navigation in Expo Router — a session context/provider plus a `_layout` that redirects on auth state — reusing my React context skills. Make me wire protected routes so unauthenticated users only see sign-in."
13. Stage 6 — Full loop: "Walk me through assembling the full Visual Life Archive loop — capture → upload to Storage → save metadata to the DB → render the grid from the DB — with loading/error/empty states. Have me design the data flow end to end and critique it."
