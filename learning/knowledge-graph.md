# Knowledge graph — what Allen actually knows

The map of my knowledge, updated after every lesson; quizzes are chosen from it.

**Ladder:** `seed` (not yet taught) → `introduced` (explained once) → `practicing`
(used it with help) → `understood`.
**`understood` means:** for a buildable thing (a loop, a function, an API route) I
wrote it unaided at least once — a passed quiz is not enough; for a purely conceptual
thing, explaining it in my own words + passing a quiz is enough.
**Rules:** statuses only upgrade on recorded evidence; don't re-quiz concepts that
are `understood` and fresh. Anything walked through and checked during planning
(2026-08-01) starts at `introduced`, not `seed`.

## Low-level: the JavaScript itself

| Concept | Status | Introduced | Reviewed | Evidence |
|---|---|---|---|---|
| Variables (`const`/`let`) | seed | — | — | — |
| Functions & arrow functions | seed | — | — | — |
| Conditionals & boolean logic | seed | — | — | — |
| Loops & array methods (`map`, `forEach`, `filter`) | seed | — | — | — |
| Objects & arrays as data shapes | seed | — | — | — |
| Template literals | seed | — | — | — |
| Destructuring & spread | seed | — | — | — |
| Closures (functions remembering their surroundings) | seed | — | — | — |
| Promises & `async`/`await` | seed | — | — | — |
| JSON (`parse`/`stringify`) | seed | — | — | — |
| Regular expressions (the email check) | seed | — | — | — |
| Animation math: normalize, clamp, lerp | seed | — | — | — |
| Events & listeners | seed | — | — | — |
| The DOM (the page as a live object tree) | seed | — | — | — |

## Structural: files, dependencies, frameworks, browser APIs

| Concept | Status | Introduced | Reviewed | Evidence |
|---|---|---|---|---|
| ES modules (`import`/`export`) | seed | — | — | — |
| `package.json` & dependencies | introduced | 2026-08-01 | — | defined in trunk (piece 2); toolchain quiz never answered — re-ask in Section 1 |
| `node_modules` & the lockfile | seed | — | — | — |
| Vite: dev server + bundling | introduced | 2026-08-01 | — | defined in trunk; no learner evidence yet |
| JSX | introduced | 2026-08-01 | — | defined during stack decisions; no learner evidence yet |
| React components & props | introduced | 2026-08-01 | — | defined in trunk (piece 5) |
| React's core idea: UI as a function of state | introduced | 2026-08-01 | 2026-08-01 | quiz: gave co-location answer; corrected to "React does the DOM bookkeeping" — re-probe in Section 3 |
| State & `useState` | introduced | 2026-08-01 | — | defined in trunk; not yet used |
| `useEffect` (run code when a component appears) | introduced | 2026-08-01 | — | one-line definition only |
| Refs (`useRef`, `forwardRef`) | seed | — | — | — |
| `IntersectionObserver` | introduced | 2026-08-01 | — | one-line definition in trunk |
| `requestAnimationFrame` | introduced | 2026-08-01 | — | one-line definition in trunk |
| `localStorage` & client-side persistence | introduced | 2026-08-01 | 2026-08-01 | quiz ✅: "the order lives on the client device only" — limitation nailed; API itself untaught |
| The `<video>` element & `currentTime` scrubbing | seed | — | — | — |
| Pointer & keyboard events | seed | — | — | — |
| `matchMedia` (reading user prefs from JS) | seed | — | — | — |
| Tailwind utilities & design tokens | introduced | 2026-08-01 | 2026-08-01 | quiz: "streamline" → sharpened to "defined once, in one place, by name"; confirmed "got it" |
| Single source of truth (`copy.js` pattern) | seed | — | — | — |
| HTTP request/response & `fetch` | seed | — | — | — |
| What a backend is (server answering requests) | introduced | 2026-08-01 | — | defined during stack decisions (Express) |
| Client vs server: where code runs | introduced | 2026-08-01 | 2026-08-01 | strong: localStorage answer + "GitHub Pages is for static sites" ✅ — confirm as understood in Section 8 |
| SQL & database tables | introduced | 2026-08-01 | — | defined during stack decisions (SQLite) |
| SQLite vs hosted DB (free-tier disk caveat) | introduced | 2026-08-01 | — | caveat explained; no learner evidence yet |
| Environment variables | seed | — | — | — |

## Engineering practice

| Concept | Status | Introduced | Reviewed | Evidence |
|---|---|---|---|---|
| Git: commits as snapshots, history | practicing | 2026-08-01 | 2026-08-01 | ran + interpreted real output with help: explained `git log` fatal (no commits) and untracked ("changes aren't yet getting monitored"); staging area introduced, first commit still pending |
| GitHub: remotes & push | introduced | 2026-08-01 | — | defined in trunk; not yet done |
| `.gitignore` | seed | — | — | — |
| CI/CD: GitHub Actions push→build→publish chain | introduced | 2026-08-01 | 2026-08-01 | quiz ❌: "the repo scans and updates" — 5-step chain taught; MUST re-check hands-on at end of Section 1 |
| Static hosting & GitHub Pages | introduced | 2026-08-01 | 2026-08-01 | quiz ✅: "GitHub Pages is for static sites" |
| SPA (single-page application) | introduced | 2026-08-01 | — | used the term correctly unprompted |
| Form validation UX (inline errors, states) | seed | — | — | — |
| Accessibility: ARIA, keyboard, focus | introduced | 2026-08-01 | — | defined in trunk (piece 7) |
| Reduced-motion & resilient fallbacks | introduced | 2026-08-01 | — | defined in trunk (piece 7) |
| Manual QA & browser DevTools | seed | — | — | — |
| Automated testing | seed | — | — | not in the 9 sections; introduce opportunistically once features exist |
| Stack tradeoffs: one language at a time (JS before TS) | understood | 2026-08-01 | 2026-08-01 | quiz ✅ own words: "becoming better with one language at a time is more important now" (conceptual → understood) |
| Choosing boring technology | introduced | 2026-08-01 | — | pattern named across all 6 decisions; Express-"easier" answer corrected to same-language reasoning |

## AI-era practice

| Concept | Status | Introduced | Reviewed | Evidence |
|---|---|---|---|---|
| Agent memory files (`CLAUDE.md`, `project.md`) | introduced | 2026-08-01 | — | directed their creation; can't yet explain load order/purpose unprompted |
| Writing a good plan (sections → deliverables) | introduced | 2026-08-01 | — | co-built plan.md; re-planned once with an updated step |
| Learning contract & answer-key discipline | introduced | 2026-08-01 | — | contract authored and enforced this session |
| Knowledge tracking (this file's ladder) | introduced | 2026-08-01 | — | created 2026-08-01 |
| Writing a spec before code | seed | — | — | starts mattering in Section 3+ |
| Reviewing a diff | seed | — | — | first real diff review comes with Section 1's first commit |
