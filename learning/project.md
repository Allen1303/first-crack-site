# Project brief — read this first, every session

## Who I am

I'm Allen. I'm comfortable with JavaScript **syntax** but not yet fluent — I want to
get genuinely better at JS through this project. React is still a little new to me;
I've had some exposure to the syntax (components, JSX) but haven't internalized the
patterns. Pitch explanations at that level: don't re-explain `const` or arrow
functions, do explain hooks, refs, closures-in-effects, and browser APIs
(`requestAnimationFrame`, `IntersectionObserver`) when they first come up.

## The learning contract (one line)

**I hand-write all the code; Claude explains, specs, hints, quizzes, and reviews, but
never authors code for me to copy — and scaffolding fades from fill-in-the-blank
early to whole-file-from-spec by the end.**

## The project idea

Rebuild, by hand, a finished demo: a one-page cinematic marketing site for a fictional
local coffee roaster, **"First Crack Roasting Co."** The signature feature is a
"scroll-film": six AI-generated video clips stacked in a sticky full-viewport canvas
over a tall (900vh) scroll track, scrubbed frame-by-frame with the scroll wheel so the
whole page plays like one continuous camera shot. Captions fade in at each clip seam,
labeled by *time since roast*. After the film come a landing beat, a press-and-hold
"Bloom" interaction (hold the cup and tasting notes spread through it like ink), a
price-justification section, an order form, and a footer — plus a fixed header and a
floating CTA bar.

Stack (decided by the demo, not up for renegotiation): **Vite + React 19, plain JSX
(no TypeScript), Tailwind CSS v4** (design tokens in `@theme`, custom `@utility`
classes, no vanilla stylesheets). Deployed to GitHub Pages via a GitHub Actions
workflow.

## In the MVP

The demo already decided scope. Everything below exists in the demo and is in:

- Vite + React 19 + Tailwind v4 project setup; design tokens (colors, three font
  stacks) in `@theme`; custom utilities `stamp`, `display-head`, `caption`/`caption-on`;
  a global `:focus-visible` style.
- **The scroll-film engine** (`Film`): 6 stacked `<video>` elements in a sticky
  full-viewport container over a 900vh section; a `requestAnimationFrame` loop maps
  scroll progress → clip index + timestamp and scrubs `currentTime` — lerping small
  deltas for smoothness, snapping jumps > ~1.2s to avoid seek storms.
- **Lazy loading**: clips 1–2 preload up front; clips 3–6 load one segment ahead of
  the scroll position.
- **Fallback mode**: `prefers-reduced-motion`, `Save-Data`, or any video load error
  swaps the film for still keyframe sections carrying the same copy.
- **Captions** timed to windows just after each seam; all copy lives in `src/copy.js`
  as the single source of truth (shared by film and fallback).
- **The Bloom** (`Bloom`): press-and-hold button (pointer *and* keyboard) with an rAF
  progress loop — hold ~1.6s and three tasting-note ink blots bloom; release early
  and it settles back; reduced-motion users see the finished state immediately.
- **Header**: fixed, brand + stamp, desktop nav, tablet CTA pill, phone hamburger
  opening a full-screen menu.
- **Landing** and **Worth** sections (copy-driven; Worth does the $18 → 72¢/cup math).
- **Floating CTA bar** (`CtaBar` + logic in `App`): appears after ~34% of the film,
  hides while the order form is on screen (`IntersectionObserver` + scroll listener).
- **Order form**: name/email with custom validation + inline error messages, radio
  groups for pickup/delivery and whole-bean/ground, busy state, success ("You're in.")
  state; **demo mode** persists orders to `localStorage`, with an `ORDER_ENDPOINT`
  constant ready to point at a real backend.
- **Accessibility throughout**: aria labels, `aria-live` status, ≥44px touch targets,
  visible focus, reduced-motion handling.
- **Deploy**: GitHub Pages via `.github/workflows/deploy.yml` on push to `main`;
  correct Vite `base` path.
- Reuse the demo's finished media assets as-is (clips, keyframes, posters) and its QA
  pages (`verify-seams.html`, `mobile-test.html`) — those aren't code to rewrite.

## Parking lot (v2)

Things the demo itself deliberately stubs or leaves out — do not build these in the MVP:

- A real order backend (`ORDER_ENDPOINT` is empty; localStorage is the demo mode).
- Payments/checkout (the "$18" button reserves, it doesn't charge).
- Real emails (the copy promises a roast-date email; nothing sends one).
- A real business: brand is a placeholder; the footer's "Visit the roastery" link is
  intentionally dead (`href="#"` + `preventDefault`).
- TypeScript (demo is deliberately plain JSX).
- Generating new or different video/keyframe assets.
- Anything else not in the demo: routing/multiple pages, CMS, analytics, sound.

> **Update 2026-08-01:** one parking-lot item was promoted into the build plan — a
> *minimal* orders backend (one resource, one table, one deploy: Express + SQLite on
> Render) now lands as Section 8, per the "demo is missing a layer" rule in
> `learning/plan.md`. Claude builds a small reference version first (same read-only
> answer-key rules as `demo/`), then I rebuild it. Payments, emails, and the rest of
> the list stay parked.

## Folder layout

```
~/Documents/learning-project/
├── demo/     ← the finished reference implementation (READ-ONLY answer key)
└── build/    ← my rebuild — all new code goes here (this git repo)
    └── learning/
        └── project.md   ← this file
```

**Demo path:** `/Users/allenarcher/Documents/learning-project/demo`
**GitHub username:** `allen1303`

## Rules for using the demo

The demo is a **read-only answer key**. Claude may read it to write specs, design
exercises, and review my work against it — but must **not show me demo code for any
piece until I've attempted that piece myself**. After my attempt, comparing my version
to the demo's is fair game and encouraged. Never edit anything under `demo/`.

## The trunk — the 8 core pieces, end to end

The map of everything I need to learn and build to ship this, drawn from what's
actually in the demo. Plain-language definitions on first use; depth comes later,
piece by piece.

1. **Source control — Git and GitHub.** Git is a tool that takes snapshots
   ("commits") of my code as I go, so I can see history, undo mistakes, and explain
   what changed and why. GitHub is a website that stores a copy of that history
   online. This project needs it from day one as the professional safety net — and
   because the finished site literally deploys *from* GitHub.

2. **The toolchain — Node, npm, and Vite.** Node is a program that runs JavaScript
   on my computer (not just inside a browser). npm is its package manager — a tool
   that downloads libraries ("packages": code other people wrote) my project depends
   on. Vite is the build tool: while I work it runs a dev server (a small local
   program that serves my site at a `localhost` address and refreshes on save), and
   at the end it bundles everything into plain optimized files a browser can load.
   The demo is a Vite project; nothing runs without this layer.

3. **Page structure and styling — HTML and Tailwind CSS.** HTML is the markup that
   says what's *on* the page (headings, buttons, forms, videos); CSS is the language
   that says how it *looks*. Tailwind is a CSS framework where styles are applied as
   small utility classes right in the markup, with the site's design decisions
   (colors, fonts) declared once as "design tokens" — named values reused everywhere.
   The demo's entire look — the stamp labels, the film captions, the dark palette —
   is built this way.

4. **JavaScript and the browser's APIs.** JavaScript is the programming language
   that makes pages interactive; my main fluency goal. An API ("application
   programming interface") is a set of built-in functions something offers you —
   here, the browser's: listening for scroll events, `requestAnimationFrame` (asking
   the browser to run my code once per screen redraw, ~60×/second), controlling a
   video's playhead, `IntersectionObserver` (the browser telling me when an element
   scrolls into view), and `localStorage` (a small key-value store in the browser).
   The scroll-film, the Bloom, and the CTA bar are all these APIs plus math.

5. **React — building the page out of components.** React is a library for building
   pages as components: reusable functions that each return a piece of the page and
   manage their own "state" (data that changes, like a menu being open). The demo is
   eight components composed in `App.jsx`, using React's hooks — functions like
   `useState` (hold changing data) and `useEffect` (run code when the component
   appears) — which is exactly the React I need to internalize.

6. **Forms and data handling.** Taking user input (the order form), validating it
   (checking the email looks like an email before accepting it), showing clear error
   and success states, and then sending it somewhere — in the MVP, saving to
   `localStorage` in "demo mode", with a marked seam where a real backend (a server
   that receives and stores orders) would plug in later.

7. **Resilience and accessibility.** Building so the site works for everyone and
   fails gracefully: keyboard operation, screen-reader labels (ARIA — attributes
   that describe elements to assistive tech), respecting a user's "reduce motion"
   setting, and falling back to still images when video can't load. The demo treats
   these as core behavior, not polish — every interactive piece has a fallback path.

8. **Deployment — GitHub Actions and GitHub Pages.** Deployment is turning my code
   into a public website. GitHub Pages is free static hosting (it serves plain
   files; no server-side code). GitHub Actions is automation that runs on GitHub's
   computers: every push to `main` triggers a workflow that builds the site with
   Vite and publishes the result — so the live site is always just "whatever is on
   `main`", which is the end-to-end payoff of pieces 1 and 2.

Rough dependency order: 1–2 first (nothing exists without them), 3–5 interleaved as
sections get built, 6–7 woven through every piece, 8 early in "hello world" form so
every later piece ships to a real URL.

## How scaffolding fades

Early pieces (setup, tokens, simple sections like Footer/Landing/Worth): near
fill-in-the-blank — Claude gives structure and I complete the blanks. Middle pieces
(Header, CtaBar, OrderForm): function-level specs with hints on request. Late pieces
(Bloom, then the Film engine — the boss fight): a written spec of behavior and edge
cases only, and I write the whole file from it. Quizzes and code review at every step.
