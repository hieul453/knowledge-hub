# Learning Roadmap: React (Core Concepts) — Phase 1

**Goal:** Understand React's core mental model — components, props, state, and effects — well enough to build small interactive UIs and to make the jump into **React Native** feel familiar. Not full React mastery; the *foundational concepts that transfer everywhere*.
**Context:** Project-based learning toward the Visual Life Archive app (Expo/React Native + Supabase). React is the mental model React Native is built on, so it comes before touching React Native itself.
**Time budget:** ~20–30 hrs of focused study + practice (on top of the JavaScript prerequisite). Flexible pace.
**Starting point:** Total beginner. Assumes you've done the JavaScript foundations first (see Prerequisites).

---

## 🗺️ Overview

React is a **library for building user interfaces out of components** — small, reusable pieces of UI that describe *what* the screen should look like for a given set of data, and let React handle *updating* the screen when that data changes. You start by understanding why that "describe, don't manipulate" idea exists (and what problem it solves), then learn to build components, feed them data with **props**, make them interactive with **state**, connect them to the outside world with **effects**, and finally structure a small app by thinking in terms of a component tree and one-way data flow. Every concept here reappears — unchanged in spirit — in React Native, so this roadmap is the real foundation for your app.

---

## ⚠️ A Note On Order (read this)

**React is JavaScript.** There is no shortcut around this. The single most common reason beginners find React confusing (props feel like magic, `.map()` in JSX is mysterious, `useState` "doesn't update") is a missing **JavaScript** foundation — not missing React knowledge. Do the JavaScript prerequisites below *first*. If you try to learn React before JS clicks, you'll be learning two hard things at once and blame React for the pain.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **JavaScript fundamentals** 🔴 — your existing JavaScript roadmap, **Stages 1–3** minimum: variables, functions, arrays/objects, and **`map`/`filter`/`reduce`** plus **`async`/`await`**. React leans on these constantly (`.map()` renders lists; `async/await` fetches data). — est. *(covered in your JS roadmap)*
- [ ] **ES6 syntax** 🔴 — arrow functions, destructuring, spread/rest, template literals, and **`import`/`export` modules**. JSX and props are built out of these; you'll see them in every React file. — est. *(part of JS Stage 1–2)*
- [ ] **Light DOM/HTML/CSS familiarity** 🟡 — what an element, tag, and CSS class are. JSX *looks* like HTML, so a little context makes it click faster. (JS roadmap Stage 4 covers the DOM.) — est. 1–2 hrs
- [ ] **Node.js + npm installed** 🟡 — needed to spin up a scratch project to practice in. — est. 30 min
> ✅ Skip any you already have. **Do not skip the JavaScript ones** — they're the foundation this entire roadmap rests on.

---

## Stage 1: What React Is & JSX — Foundation
**Goal of this stage:** Understand *why* React exists and write your first components using JSX.
**Estimated time:** 4–6 hrs
**Milestone:** You can explain, in plain language, what a component is and what "declarative UI" means, and you can write a component that renders JSX with a JavaScript variable embedded in it — running live in a scratch project.

### Must-Know Topics 🔴
- [ ] **Why React exists** — declarative UI (you describe *what* the screen should be; React updates the DOM for you) vs. manually manipulating the DOM. This is the root idea everything else builds on.
- [ ] **Components** — a component is a JavaScript function that returns markup; the capital-letter naming rule; how you build a UI by composing components.
- [ ] **JSX** — writing markup inside JavaScript, using `{ }` curly braces to embed JS expressions/variables, and `className` instead of `class`.
- [ ] **Scratch project setup** — spin up a practice app (Vite's React template is the standard) *just enough* to have somewhere to write code. Don't rabbit-hole on tooling.
### Should-Know Topics 🟡
- [ ] The difference between a React **component** and a plain HTML element (capitalization, why it matters).
### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me what React is and why it exists — declarative UI and the component model vs. manually manipulating the DOM. Quiz me until I can explain *why* React is useful in my own words."
> 2. "Teach me JSX and how to write a React component — the function-returns-markup idea, curly braces for embedding JavaScript, and the capital-letter rule. Give me small snippets and ask me to predict what renders."

---

## Stage 2: Components & Props — Composition
**Goal of this stage:** Build reusable components and pass data into them, including rendering lists.
**Estimated time:** 4–6 hrs
**Milestone:** You can build a component that receives **props** and use it to render a list of items from an array (e.g. a list of `DayCard`s, each with a date and caption) — and explain why data flows *down* from parent to child.

### Must-Know Topics 🔴
- [ ] **Props** — passing data *into* a component to customize it; props are read-only; the parent-to-child, one-way flow.
- [ ] **Composition** — nesting components inside components to build bigger UI from small pieces.
- [ ] **Rendering lists** — using `.map()` to turn an array into a list of components, and **why each item needs a `key`**.
- [ ] **Conditional rendering** — showing different UI based on data (`&&`, the ternary operator).
### Should-Know Topics 🟡
- [ ] The `children` prop — passing JSX *between* a component's tags.
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me React props and component composition — passing data parent-to-child, why props are read-only, and one-way data flow. Quiz me by giving me a UI and asking what props each component needs."
> 2. "Teach me rendering lists with `.map()` and conditional rendering in React, including why `key` matters. Give me an array and ask me to render it as components."

---

## Stage 3: State & Interactivity 🧠
**Goal of this stage:** Make components interactive — hold data that changes over time and re-render when it does.
**Estimated time:** 5–7 hrs (slow down here — this is where React "clicks" or doesn't)
**Milestone:** You can build an interactive component (a counter, and a controlled text input for a caption) using `useState`, handle events, and explain *why* changing state re-renders the component while a plain variable wouldn't.

### Must-Know Topics 🔴
- [ ] **`useState`** — creating state that, when changed, tells React to re-render; why you must use the setter (not reassign a variable).
- [ ] **The render mental model** — state change → re-render → UI reflects new state. This is *the* core loop.
- [ ] **Handling events** — `onClick`, `onChange`, and passing event handler functions.
- [ ] **Controlled inputs / forms** — tying an input's value to state so React is the single source of truth (directly relevant to your caption field).
### Should-Know Topics 🟡
- [ ] State is a **snapshot** — why `setCount(count + 1)` twice doesn't add 2, and the updater-function form `setCount(c => c + 1)`.
- [ ] Where state should live — keep it in the component that needs it (sets up "lifting state up" in Stage 5).
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me React state with `useState` — what it is, why changing state re-renders, and why I can't just use a normal variable. Quiz me hard with snippets and ask me to predict what renders after each state change."
> 2. "Teach me handling events and controlled form inputs in React — tying an input to state. Give me a small form and make me wire it up correctly."

---

## Stage 4: Side Effects & Data
**Goal of this stage:** Connect components to the outside world — fetch data and react to changes — with `useEffect`.
**Estimated time:** 4–6 hrs
**Milestone:** You can fetch data from a public API when a component loads and correctly show **loading**, **error**, and **success** states.

### Must-Know Topics 🔴
- [ ] **`useEffect`** — running code *after* render (on mount, or when a dependency changes), and the **dependency array** and why it matters.
- [ ] **Fetching data** — calling an API inside an effect, storing the result in state, and rendering it.
- [ ] **Loading & error states** — conditional rendering applied to the reality that network calls take time and can fail (your Stage 2 + 3 skills converge here).
### Should-Know Topics 🟡
- [ ] Effect **cleanup** — returning a function from an effect and why (light touch).
- [ ] Modern nuance: in current React, `useEffect` is a *last resort*, not the default tool for everything — but it's still a must-know core concept, and you'll meet it constantly. Learn it now; learn when to *avoid* it later.
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me `useEffect` in React — running code after render, the dependency array, and cleanup. Quiz me on when an effect re-runs given different dependency arrays."
> 2. "Teach me fetching data from an API inside a React component and handling loading and error states. Give me an endpoint and make me build the loading/error/success UI."

---

## Stage 5: Thinking in React — Composition & Data Flow
**Goal of this stage:** Move from "isolated components that work" to structuring a small app: where state lives and how data flows.
**Estimated time:** 3–5 hrs
**Milestone:** Given a simple UI mockup, you can break it into a component tree, decide *where each piece of state should live*, and wire it together with props down / events up.

### Must-Know Topics 🔴
- [ ] **One-way data flow** — props flow *down*; to change a parent's state from a child, the parent passes a function *down* and the child calls it (events "up").
- [ ] **Lifting state up** — when two components need the same data, move that state to their closest common parent.
- [ ] **Decomposing a UI into a component tree** — the official "Thinking in React" exercise applied to a real screen.
### Should-Know Topics 🟡
- [ ] **`useRef`** — holding a value across renders without causing a re-render (light introduction).
- [ ] **`useContext`** — sharing state across many components without passing props through every level (you'll use this for things like the logged-in user later).
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me one-way data flow and lifting state up in React — props down, events up. Give me a scenario with two sibling components that share data and make me decide where the state goes."
> 2. "Walk me through 'Thinking in React' — decomposing a UI mockup into a component tree and placing state correctly. Give me a mockup and make me do it, then critique my answer."

---

## 🏁 Final Milestone
You can build a small interactive React app from scratch — components composed into a tree, data passed via props, interactivity via state and events, data fetched with effects, and state placed correctly with proper one-way data flow — **and** explain *why* React re-renders, *why* props are read-only, and *why* the component model exists. At that point React Native will feel like "React with different building blocks," which is exactly the launchpad you want.

---

## ⏭️ What's Out of Scope (For Now)
- **React Native itself** — the whole point of this roadmap is to prepare for it, but RN is its **own separate roadmap** (your Group 2). Finish this first; the concepts carry over directly.
- **Web-specific tooling deep-dives** (Vite config, bundlers, Webpack, Babel) — you only need enough setup to practice. Don't rabbit-hole.
- **Routing (React Router), Next.js, Server Components, Suspense** — powerful, but web-app concerns you don't need for the mobile-first goal. Revisit if/when you build the *web* version.
- **State management libraries (Redux, Zustand)** — you won't need them at this scale; `useState`/`useContext` are plenty.
- **Performance optimization (`useMemo`, `useCallback`, `React.memo`)** — modern React's compiler handles most of this automatically now; learn it only if you hit a real performance problem.
- **TypeScript with React** — worth adding *after* the concepts are solid (it's a layer on top, not a foundation). Flagged in your stack as the language you'll ultimately write in.
- **Custom hooks & `useReducer`** — intermediate patterns; revisit once the core hooks are second nature.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Why React: "Teach me what React is and why it exists — declarative UI and the component model vs. manually manipulating the DOM. Quiz me until I can explain *why* React is useful in my own words."
2. Stage 1 — JSX: "Teach me JSX and how to write a React component — function-returns-markup, curly braces for embedding JavaScript, and the capital-letter rule. Give me snippets and ask me to predict what renders."
3. Stage 2 — Props: "Teach me React props and component composition — parent-to-child data, why props are read-only, one-way flow. Quiz me on what props each component needs."
4. Stage 2 — Lists: "Teach me rendering lists with `.map()` and conditional rendering, including why `key` matters. Give me an array to render as components."
5. Stage 3 — State: "Teach me React state with `useState` — why changing state re-renders and why a normal variable won't. Quiz me hard with snippets; make me predict what renders."
6. Stage 3 — Events/forms: "Teach me handling events and controlled form inputs in React. Give me a small form and make me wire it up correctly."
7. Stage 4 — useEffect: "Teach me `useEffect` — running code after render, the dependency array, and cleanup. Quiz me on when an effect re-runs."
8. Stage 4 — Data fetching: "Teach me fetching data from an API in a React component and handling loading and error states. Give me an endpoint and make me build the UI."
9. Stage 5 — Data flow: "Teach me one-way data flow and lifting state up — props down, events up. Give me two sibling components sharing data and make me place the state."
10. Stage 5 — Thinking in React: "Walk me through 'Thinking in React' — decomposing a mockup into a component tree and placing state. Give me a mockup and critique my answer."
