# Learning Roadmap: Flexbox (Layout & Styling) — Phase 1

**Goal:** Understand Flexbox deeply enough to lay out any screen with confidence — not by guessing which property to add until it looks right, but by *knowing* how the container/item model and the two-axis system decide where things go. The payoff is being able to build the Visual Life Archive's layouts (a day-card list/gallery, a capture screen) in React Native, and reuse the exact same knowledge on the web version.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). Flexbox *is* the layout system in React Native, and the dominant one-dimensional layout tool on the web — so it serves both halves of your stack.
**Time budget:** ~9–13 hrs of focused study + practice. Flexible pace.
**Starting point:** Total beginner at layout. Flexbox is universal, so you can learn it in a plain browser sandbox first, then apply it in React Native — this roadmap does exactly that.

---

## 🗺️ Overview

Flexbox is a layout model built on one simple idea: you mark an element as a **flex container**, and its direct children become **flex items** that you arrange along a **main axis** and a **cross axis**. Almost every confusion with Flexbox comes from not internalizing those two axes — so this roadmap starts there, then builds outward: first *aligning and distributing* items along the axes, then *sizing* them (grow / shrink / basis — the part everyone finds mysterious), and finally *assembling real layouts* and learning where React Native's flexbox differs from the web's. You'll practice on the web (fast feedback, great tools) and finish by building an actual screen layout for your app.

---

## ⚠️ A Note On Where You'll Practice (read this)

Flexbox behaves *almost* identically on the web and in React Native — same axes, same core properties — with a few RN-specific defaults (covered in Stage 4). Because the web has instant feedback (browser DevTools, live editors, the Flexbox Froggy game), **learn the model in a browser first**, then apply it in React Native. Don't try to learn Flexbox and React Native styling syntax at the same time; learn the *concept* where it's easiest to see, then port it. The concept transfers 1:1.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **Basic HTML & CSS familiarity** 🟡 — what an element is, and how to apply a CSS rule (a selector + `property: value`). Enough to open a live editor and style a `<div>`. This is only for the *practice sandbox* — you don't need CSS depth. — est. 1–2 hrs
- [ ] **React (core concepts)** 🟡 — only needed when you reach the React Native application in Stage 4 (styles are just objects passed to components). You can start Stages 1–3 without it. — est. *(covered in your React roadmap)*
> ✅ Skip either if you already have it. Neither gates Stages 1–3 — you can start Flexbox today in a browser editor.

---

## Stage 1: The Mental Model — Container, Items & the Two Axes
**Goal of this stage:** Build the core mental model so every later property makes sense: what a flex container/item is, and how the main axis and cross axis work.
**Estimated time:** 2–3 hrs
**Milestone:** Given any `flex-direction`, you can point to which axis is the main axis and which is the cross axis, and explain why that determines what every other property does.

### Must-Know Topics 🔴
- [ ] **Flex container vs flex items** — `display: flex` turns an element into a container; its *direct* children become items (grandchildren are not affected)
- [ ] **The main axis and the cross axis** — the single most important concept; every flex property acts on one axis or the other
- [ ] **`flex-direction`** — `row` / `column` (and the `-reverse` variants); this sets which direction is the main axis, flipping how everything else behaves
- [ ] **React Native preview** 🔴 — in RN, every `View` is *already* a flex container, and the default `flexDirection` is **`column`** (on the web it's `row`). Same axes, different default. (Full RN differences in Stage 4.)
### Should-Know Topics 🟡
- [ ] Why Flexbox is "direction-agnostic" — it adapts to content and screen size, unlike older block/inline flow
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me the Flexbox mental model — flex container vs flex items, and the main axis vs cross axis. Quiz me by giving me a `flex-direction` and asking which axis is which and what that implies."
> 2. "Teach me `flex-direction` and how switching between row and column changes which axis is the main axis. Include the React Native default (column) vs web default (row). Give me snippets and make me predict the layout."

---

## Stage 2: Distributing & Aligning — justify-content, align-items, align-self
**Goal of this stage:** Position items along both axes — including the classic "center a box perfectly" — using the alignment properties.
**Estimated time:** 2–3 hrs
**Milestone:** You can center content both horizontally and vertically, spread items evenly with `space-between` / `space-around` / `space-evenly`, and align a single item differently from its siblings.

### Must-Know Topics 🔴
- [ ] **`justify-content`** — distributes items along the **main** axis (`flex-start`, `center`, `space-between`, `space-around`, `space-evenly`); note it only does something when there's spare space on the main axis
- [ ] **`align-items`** — aligns items along the **cross** axis (`stretch` default, `flex-start`, `center`, `baseline`)
- [ ] **`align-self`** — override `align-items` for one individual item
- [ ] **Perfect centering** — `justify-content: center` + `align-items: center`; understand *why* it works (one property per axis)
### Should-Know Topics 🟡
- [ ] How `flex-direction` swaps what `justify-content` and `align-items` control — because they're tied to axes, not to "horizontal/vertical"
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `justify-content` (main axis) and `align-items` (cross axis), including all the `space-*` values and `align-self`. Quiz me by describing a layout and asking which properties produce it."
> 2. "Drill me on centering with Flexbox and on how changing `flex-direction` flips what `justify-content` vs `align-items` do. Give me a target layout and make me write the properties."

---

## Stage 3: Sizing & Flexibility — grow, shrink, basis & wrapping
**Goal of this stage:** Master the "flexible" part of Flexbox — how items grow to fill space, shrink to avoid overflow, and wrap onto new lines. This is the part most people never fully understand; slow down here.
**Estimated time:** 3–4 hrs
**Milestone:** You can build a row where items share leftover space in the proportions you intend, shrink gracefully instead of overflowing, and wrap onto multiple lines on a narrow screen.

### Must-Know Topics 🔴
- [ ] **`flex-grow`** — how items *take up* extra free space, and how the unitless numbers act as proportions
- [ ] **`flex-shrink`** — how items *give up* space to avoid overflow
- [ ] **`flex-basis`** — an item's starting size *before* grow/shrink apply; how it differs from `width`/`height`
- [ ] **The `flex` shorthand** — `flex: grow shrink basis`; the ubiquitous **`flex: 1`** idiom ("share space equally / fill available space"), extremely common in React Native
- [ ] **`flex-wrap`** — letting items wrap to new lines instead of shrinking forever (essential for a responsive card gallery)
### Should-Know Topics 🟡
- [ ] **`gap`** — clean spacing *between* items without margins (supported on the web and in modern React Native)
- [ ] **`align-content`** — how *multiple wrapped lines* are distributed on the cross axis (only matters once items wrap)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `flex-grow`, `flex-shrink`, and `flex-basis` from the ground up — what each does and how the `flex` shorthand combines them. Quiz me hard: give me containers with set sizes and make me predict each item's final size, including `flex: 1`."
> 2. "Teach me `flex-wrap`, `gap`, and `align-content` for multi-line layouts. Give me a set of cards and a container width and make me predict how they wrap and space out."

---

## Stage 4: Real Layouts & React Native Differences
**Goal of this stage:** Assemble everything into real screen layouts, and learn exactly how Flexbox in React Native differs from the web so you can apply your knowledge in your app.
**Estimated time:** 2–3 hrs
**Milestone:** You can build the Visual Life Archive's core layouts in React Native — a vertical screen (header / scrollable content / footer) and a wrapping day-card gallery — using only Flexbox, and explain each RN-vs-web difference.

### Must-Know Topics 🔴
- [ ] **Composing real layouts** — the common patterns: a full-height column (header + flexible content + footer), a horizontal row of cards, and a wrapping grid-like gallery of `DayCard`s
- [ ] **React Native flexbox differences** 🔴 — `View` is a flex container by default; default `flexDirection` is **`column`**; you write styles as **objects with camelCase keys** (`flexDirection`, `justifyContent`, `alignItems`) via `StyleSheet.create`; dimensions are **unitless** (density-independent pixels, no `px`); **Flexbox is the *only* layout system** — there is no `float` and no CSS Grid in RN
- [ ] **`flex: 1` to fill the screen** — the RN idiom for "make this View take all remaining space"
### Should-Know Topics 🟡
- [ ] **`aspect-ratio`** — keeping image cards a consistent shape (very handy for a photo gallery)
- [ ] Where Flexbox stops on the web → **CSS Grid** for true 2-D layouts (awareness only; RN has no grid, so you stay in Flexbox there)
### Nice-to-Know Topics 🟢
- [ ] The `order` property (web) — visually reorder items without changing markup
- [ ] `min-width` / `min-height` and how they interact with shrinking (the classic "why won't my item shrink?" gotcha)
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me to build real layouts with Flexbox — a full-height header/content/footer column and a wrapping card gallery. Give me a target screenshot in words and make me write the flex properties."
> 2. "Teach me every way React Native's Flexbox differs from the web — default column direction, camelCase style objects, unitless sizes, flexbox-only layout, `flex: 1`. Quiz me by giving me web CSS and making me translate it to React Native styles."

---

## 🏁 Final Milestone
You can look at any screen design and build its layout with Flexbox without trial-and-error — placing items on the right axis, distributing and aligning them, and sizing them with grow/shrink/basis and wrapping — **and** explain *why* each property behaves as it does in terms of the container/item model and the two axes. You can do this in both a browser and React Native, and you can translate a web flex layout into RN styles on sight. Concretely: you can build the Visual Life Archive's day-card gallery and capture screen from scratch.

---

## ⏭️ What's Out of Scope (For Now)
- **CSS Grid** — the two-dimensional layout system; complements Flexbox on the web but **doesn't exist in React Native**. Worth a short separate roadmap later *for the web version only*.
- **The rest of CSS** — the box model in depth, positioning (`absolute`/`relative`/`sticky`), transitions/animations, media/container queries. Related to layout but separate topics; learn as needed.
- **NativeWind / Tailwind / styled-components in RN** — styling *abstractions* built on top of raw flexbox styles. Learn raw Flexbox first (this roadmap); adopt an abstraction later only if you want one.
- **Responsive web design beyond wrapping** (breakpoints, media queries, fluid typography) — a web-layout topic that builds on Flexbox; revisit when you build the web version.
- **React Native styling beyond layout** (theming, platform-specific styles, `Dimensions`, safe areas) — belongs in the React Native roadmap, not here.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Mental model: "Teach me the Flexbox mental model — flex container vs flex items, and the main axis vs cross axis. Quiz me by giving me a `flex-direction` and asking which axis is which and what that implies."
2. Stage 1 — flex-direction: "Teach me `flex-direction` and how switching between row and column changes which axis is the main axis. Include the React Native default (column) vs web default (row). Give me snippets and make me predict the layout."
3. Stage 2 — Alignment: "Teach me `justify-content` (main axis) and `align-items` (cross axis), including all the `space-*` values and `align-self`. Quiz me by describing a layout and asking which properties produce it."
4. Stage 2 — Centering/axis-swap: "Drill me on centering with Flexbox and on how changing `flex-direction` flips what `justify-content` vs `align-items` do. Give me a target layout and make me write the properties."
5. Stage 3 — Grow/shrink/basis: "Teach me `flex-grow`, `flex-shrink`, and `flex-basis` from the ground up and the `flex` shorthand. Quiz me hard: give me sized containers and make me predict each item's final size, including `flex: 1`."
6. Stage 3 — Wrapping/gap: "Teach me `flex-wrap`, `gap`, and `align-content` for multi-line layouts. Give me cards and a container width and make me predict how they wrap and space out."
7. Stage 4 — Real layouts: "Teach me to build real layouts with Flexbox — a full-height header/content/footer column and a wrapping card gallery. Describe a target layout and make me write the flex properties."
8. Stage 4 — RN differences: "Teach me every way React Native's Flexbox differs from the web — default column, camelCase style objects, unitless sizes, flexbox-only layout, `flex: 1`. Give me web CSS and make me translate it to React Native styles."
