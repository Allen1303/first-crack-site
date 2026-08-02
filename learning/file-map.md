# File map — no mystery boxes

Every file and folder, one line each: what it is and why it exists.
**Marks:** `known` (I explained it in my own words) · `parked` (honest one-liner
now, deep dive scheduled) · `generated` (machine-made, never edit) ·
`not-yet-authored` (exists in the demo as the target shape; doesn't exist in
`build/` until I write it).

## In build/ today

| Path | Mark | What / why |
|---|---|---|
| `CLAUDE.md` | known | Standing orders every Claude session reads: coach, don't author; demo is a hidden answer key. |
| `learning/project.md` | known | The brief: who I am, scope (MVP + parking lot), contract, trunk, folder rules. Read first, every session. |
| `learning/plan.md` | known | Locked stack decisions with my evidence, and the 9-section build plan. |
| `learning/knowledge-graph.md` | known | Ladder of every concept (seed→introduced→practicing→understood); drives what I get quizzed on. |
| `learning/file-map.md` | known | This file — one honest line per file, so nothing in my repo is a mystery box. |
| `.git/` | generated | Git's internal database of commits; managed entirely by git commands, never edited by hand. |

### Scaffolded 2026-08-01 by `create-vite` (contract override on Task 1.2 — toured, not hand-written)

| Path | Mark | What / why |
|---|---|---|
| `package.json` | parked → tour in progress | The project ID card the scaffolder wrote instead of me: name, scripts, dependencies. I owe a line-by-line read against the spec I was going to write. |
| `package-lock.json` | generated | Exact frozen versions of the whole dependency chain; npm's, never edited. |
| `node_modules/` | generated | The installed packages (100+, transitive); regenerable, never committed. |
| `.gitignore` | parked | The scaffolder's list of what git must never track (`node_modules`, `dist`…); read it in Task 1.4. |
| `index.html` | parked | The single real HTML page; loads `src/main.jsx`. Deep dive in Task 1.3. |
| `vite.config.js` | parked | Vite settings: React plugin now; Tailwind + Pages `base` added later. Deep dive in 1.3/1.6. |
| `src/main.jsx` | parked | JS entry point: mounts React onto the HTML page. Deep dive in Task 1.3. |
| `src/App.jsx` | parked | Scaffolder's demo counter component — gets replaced by my own code in Task 1.3. |
| `src/App.css`, `src/index.css` | parked | Scaffolder's demo styles; replaced wholesale by the Tailwind setup in Section 2. |
| `src/assets/` (`react.svg`, `vite.svg`, `hero.png`) | parked | Demo images the template ships; deleted with the boilerplate in 1.3. |
| `public/favicon.svg`, `public/icons.svg` | parked | Template's browser-tab icon + icon sprite; favicon gets replaced with our own eventually. |
| `eslint.config.js` | parked | Config for ESLint, a code-mistake linter the scaffolder includes; honest one-liner for now, revisit if we adopt linting. |
| `README.md` | parked | Scaffolder boilerplate text; rewritten in my own words at end of Section 1. |

## Target shape — from the demo, not yet authored in build/

The demo at `~/Documents/learning-project/demo` is the finished shape this repo grows
into. Everything below is `not-yet-authored` until I write it (section that creates
it in parentheses); demo-only files that never get copied are marked as such.

| Path | Mark | What / why |
|---|---|---|
| `package.json` | not-yet-authored (S1) | The project's ID card: name, scripts (`dev`, `build`), and its list of dependencies. |
| `package-lock.json` | generated (S1) | npm's exact record of every installed package version, so installs are reproducible; machine-made. |
| `node_modules/` | generated (S1) | The downloaded packages themselves; never edited, never committed (that's what `.gitignore` is for). |
| `.gitignore` | not-yet-authored (S1) | Tells git which files to never track (e.g. `node_modules/`, `dist/`). |
| `index.html` | not-yet-authored (S1) | The single real HTML page; loads fonts and the JS entry point. |
| `vite.config.js` | not-yet-authored (S1) | Vite's settings — React plugin, Tailwind plugin, the `base` path GitHub Pages needs. |
| `.github/workflows/deploy.yml` | not-yet-authored (S1) | The CI/CD recipe: on push to `main`, build the site and publish to Pages. |
| `README.md` | not-yet-authored (S1, grows over time) | The repo's front-door explanation for humans. |
| `src/main.jsx` | not-yet-authored (S1) | The JS entry point: mounts the React app into the HTML page. |
| `src/index.css` | not-yet-authored (S2) | The only stylesheet: Tailwind import, design tokens in `@theme`, custom utilities. |
| `src/copy.js` | not-yet-authored (S2) | Single source of truth for all film captions and copy. |
| `src/App.jsx` | not-yet-authored (S1, grows S2–S6) | Root component: composes all sections; owns the CTA-bar visibility logic. |
| `src/components/Landing.jsx` | not-yet-authored (S2) | Simple copy section: the landing beat after the film. |
| `src/components/Worth.jsx` | not-yet-authored (S2) | The "$18 → 72¢ a cup" price-math section. |
| `src/components/Footer.jsx` | not-yet-authored (S2) | Address, hours, brand line. |
| `src/components/Header.jsx` | not-yet-authored (S3) | Fixed header: brand, nav, mobile full-screen menu (`useState`). |
| `src/components/CtaBar.jsx` | not-yet-authored (S3) | Floating order button; appears mid-film, hides at the form. |
| `src/components/OrderForm.jsx` | not-yet-authored (S4) | Validation, error/success states, localStorage demo mode, `ORDER_ENDPOINT` seam. |
| `src/components/Bloom.jsx` | not-yet-authored (S5) | Press-and-hold ink-bloom interaction (pointer + keyboard + rAF). |
| `src/components/Film.jsx` | not-yet-authored (S6) | The boss fight: scroll-scrubbed six-clip film engine with captions, lazy loading, fallback. |
| `public/assets/` (video/keyframes/posters) | parked | Finished media copied from the demo as-is — assets, not code; how they were generated is out of scope. |
| `public/verify-seams.html` | parked | Demo QA page showing each clip's first/last frame; used in S7, not rewritten. |
| `public/mobile-test.html` | parked | Demo QA harness (390×844 iframe) for phone layout; used in S7, not rewritten. |
| `dist/` | generated (S1+) | Vite's build output — the plain files that actually get deployed; never edited. |
| *(S8, shape TBD)* backend repo: `server.js`, `db.js`, `orders` table | not-yet-authored (S8) | The rebuilt reference backend: Express + SQLite, one resource, deployed to Render. |
| `learning/architecture.md` | not-yet-authored (S9) | Capstone: my own end-to-end explanation of how everything works. |

## Demo-only files (never copied)

| Path | Mark | What / why |
|---|---|---|
| `demo/stage1-research.md` | parked | Customer research the demo's copy was written from; background reading, not code. |
| `demo/stage2-story.md` | parked | Shot-by-shot story outline that shaped the site structure; background reading. |
