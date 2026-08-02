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
| ES modules (`import`/`export`) | practicing | 2026-08-01 | 2026-08-01 | explained `type="module"` unlocks import/export; traced the import chain (main.jsx → App.jsx, index.css) |
| The render chain (HTML → module script → React mount) | practicing | 2026-08-01 | 2026-08-01 | own words: "js finds the root div and react renders the app inside it"; wrote + rendered own App.jsx |
| Vite dev server & HMR | introduced | 2026-08-01 | 2026-08-01 | observed live: "page auto refreshed without me reloading"; HMR/websocket explained after |
| `package.json` & dependencies | introduced | 2026-08-01 | 2026-08-01 | knew the 6-field spec; read the scaffolder's real file — read-back quiz (extras vs spec) still owed at 1.3 open |
| `node_modules`, the lockfile & transitive deps | practicing | 2026-08-01 | 2026-08-01 | predicted 4 folders, got 105; explained gap unprompted: "the dependencies ask for the rest" |
| npm's project resolution (walk-up rule) | practicing | 2026-08-01 | 2026-08-01 | live incident: install landed in `~`; followed clues (`npm prefix`, prompt counter) to diagnose + clean it with guidance |
| Paths: absolute vs relative (`~`, `.`) | introduced | 2026-08-01 | — | asked "run from build/?" → taught; saw why `rm -rf` used absolute paths |
| The `--` separator convention | introduced | 2026-08-01 | — | corrected own command; then hit `git log oneline` fatal and self-fixed to `--oneline` |
| Vite: dev server + bundling | practicing | 2026-08-01 | 2026-08-01 | ran + interpreted a real build: JSX→JS ✓, explained the 189 KB ("react and react dom engine code"), fingerprints/gzip/public toured |
| JSX | introduced | 2026-08-01 | — | defined during stack decisions; no learner evidence yet |
| React components & props | practicing | 2026-08-01 | 2026-08-01 | wrote first component from spec unaided (function App, JSX return, default export); props still untouched |
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
| Git: commits as snapshots, history | practicing | 2026-08-01 | 2026-08-01 | made first two real commits (`a718398`, `42c1734`), read `git log --oneline`; earlier: explained the no-commits fatal + untracked |
| Git as a safety net (commit before risky ops) | practicing | 2026-08-01 | 2026-08-01 | canceled a scaffold mid-prompt when uncommitted, committed docs first, then re-ran — did the right sequence with prompting |
| GitHub: remotes & push | practicing | 2026-08-01 | 2026-08-01 | created + pushed real repo with gh CLI; explained push payload ("the commits not the files") |
| `.gitignore` | practicing | 2026-08-01 | 2026-08-01 | explained its effect unprompted ("gitignore keeps node_modules out"); hasn't authored one yet |
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
