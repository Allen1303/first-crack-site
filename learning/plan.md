# Build plan — learning first (v2, re-planned 2026-08-01)

Re-run with the updated planning step: **if the demo is missing a layer, build that
layer as a small reference first** (one resource, one table, one deploy), sequenced
just before the section where I rebuild it. The demo is frontend-only, so a minimal
orders backend joins the plan as Section 8 — built by Claude as a reference under the
same read-only answer-key rules as `demo/`, then rebuilt by me.

Decisions 1–3 and 6a are **demo-derived** (understand the choice, not make it).
Decisions 4, 5, and 6b are **from scratch** (the demo doesn't have this layer):
popular boring recommendation + alternatives. Status flips to ✅ once I've explained
the choice in my own words.

## Stack decisions

### 1. Language: JavaScript (plain JSX — no TypeScript)  [demo-derived] — ✅ (2026-08-01: "becoming better with one language at a time is more important now")
- **Demo uses:** plain modern JavaScript; JSX is JS with HTML-looking syntax for the page.
- **Why sensible:** JS is the only language browsers run natively; my goal is JS fluency.
- **Traded off:** *TypeScript* — type checking catches real bugs, but is a second
  syntax to learn while still cementing the first.

### 2. Frontend: React 19 + Vite  [demo-derived] — explained: ✅ (2026-08-01: co-location of HTML+JS; corrected to the deeper reason — declare UI from state, React does the DOM bookkeeping)
- **Demo uses:** React (page built from components) with Vite as dev server + bundler.
- **Why sensible:** the popular boring choice — biggest community, most beginner docs,
  most transferable skill.
- **Traded off:** *Vue/Svelte* — gentler syntax, smaller ecosystem when stuck. *No
  framework* — deepest DOM learning, but hand-managing state across 8 interacting
  sections becomes spaghetti; React exists because of that pain.
- **Key correction absorbed:** React is not *faster* than plain JS — it's a layer on
  top of it. What it buys is sanity: describe UI per state; React does the DOM
  bookkeeping.

### 3. Styling: Tailwind CSS v4  [demo-derived] — explained: ✅ (2026-08-01: tokens = defined once, in one place, by name)
- **Demo uses:** utility classes in markup; design tokens in `@theme`; custom
  `@utility` classes; no vanilla stylesheets.
- **Why sensible:** styles live next to what they style; every color/font is defined
  once, in one place, by name — consistency by default.
- **Traded off:** *plain CSS files* — rawer learning, consistency by hand. *CSS-in-JS* —
  same co-location, runtime cost, shrinking community.

### 4. Backend: Node.js + Express  [from scratch — demo has none] — explained: ✅ (2026-08-01: corrected — the argument isn't "easier," it's *same language*: JS everywhere honors one-language-at-a-time)
- **Recommendation:** Express, the boring standard web framework for Node. A
  *backend* is a program running on a server that receives requests (like "save this
  order") and answers them; Express is the minimal, most-documented way to write one.
- **Why it fits:** it keeps everything in JavaScript — the same language I'm building
  fluency in — and has two decades of beginner answers online.
- **Alternatives:** *Python + Flask* — equally boring and beloved, but a second
  language, which violates my one-language-at-a-time rule. *Fastify/Hono* — more
  modern Node frameworks, faster and cleaner, but far fewer beginner resources when
  stuck.

### 5. Database: SQLite  [from scratch — demo has none] — explained: ✅ (2026-08-01: localStorage limitation nailed — "the order lives on the client device only," so the roaster never sees it; SQLite on the server fixes that)
- **Recommendation:** SQLite — a real SQL database that lives in a single file inside
  the app, no separate database server to install or run. A *database* is organized,
  durable storage the backend reads and writes; *SQL* is the standard language for
  querying it, and the single most transferable data skill.
- **Why it fits:** one table (`orders`) is the whole need; SQLite removes every piece
  of operational overhead while still teaching real SQL.
- **Alternatives:** *Postgres* — the production standard, but it's a server of its own
  to run and connect to; overkill for one table. *MongoDB* — stores JSON documents,
  feels easy from JS, but skips SQL, and SQL is the skill worth having.
- **Honest deploy caveat:** free hosting tiers wipe their disk on each redeploy, so a
  deployed SQLite file loses rows when the backend redeploys. Accepted for a learning
  reference; the v2 fix is a hosted database (e.g. Postgres on Neon).

### 6. Hosting — two halves — explained: 🔶 half-locked (2026-08-01: "Pages is for static sites" ✅; the push→live chain was fuzzy ("repo scans and updates") — re-verify hands-on at the end of Section 1, after building the pipeline)
- **6a. Frontend: GitHub Pages via GitHub Actions.** [demo-derived] Static files,
  hosted free, deployed automatically on every push to `main` — CI/CD in its simplest
  honest form. Traded off: *Netlify/Vercel* (slicker, more magic hidden), *VPS* (full
  control, real ops burden, zero benefit for static files).
- **6b. Backend: Render free tier.** [from scratch] Pages cannot run a server — it
  only serves files — so the backend needs a host that runs Node. Render is the boring
  git-push-to-deploy choice with the gentlest docs. Alternatives: *Railway* — slicker,
  but pricing shifts; *Fly.io* — more control, more ops to learn. (Disk caveat from
  decision 5 applies.)

## The build, in 9 sections

Each section ends in something I can see working. Ladder: page → styling →
interactivity → features → backend → ship. Frontend deploy moves early (Section 1) so
everything after ships to a real URL; the backend layer lands late (Section 8), after
the frontend is whole, and fixes the localStorage limitation for real.

1. **Foundations: repo, toolchain, hello world — deployed.**
   Git from the first commit; Node/npm/Vite project I can explain file-by-file; one
   React component; Actions → Pages pipeline.
   **Deliverable:** placeholder page live at a public URL, deployed by a push.

   Tasks (each ends in something I can see working):
   - [x] **1.1 Toolchain check.** ✅ 2026-08-01 — Node v24.10.0, npm 11.6.0,
     git 2.47.1. Interpreted the empty-repo state: `git log` fatal ("because there
     are no commits yet"), untracked = "changes aren't yet getting monitored".
     Note: ran commands before predicting — hold the predict-first line next time.
   - [x] **1.2 `package.json` + install.** ✅ 2026-08-01 — **contract override
     invoked:** scaffolded with `create-vite` instead of hand-writing (explicitly
     chosen after the tradeoff was laid out twice). Detour first: accidental install
     landed in `~` via npm's walk-up rule — diagnosed from clues (`npm prefix`,
     unchanged `?2`), cleaned with targeted `rm -rf`. All 12 scaffold files toured or
     parked in the file map; 105 packages vs predicted 4 → transitive deps in own
     words ("the dependencies ask for the rest"). Commits `a718398` (docs, made
     BEFORE the risky scaffold — safety-net habit) and `42c1734` (scaffold).
     *Carried into 1.3: read-back quiz on the scaffolder's package.json extras.*
   - [x] **1.3 First render, owned.** ✅ 2026-08-01 — read-back quiz done (all six
     spec fields found in scaffolder's file; @types explained). Render chain
     translated in own words: "js finds the root div and react renders the app
     inside it." Boilerplate sweep bundled per pacing rule; first hand-written
     component (`App.jsx`, h1) rendering at localhost. Styled/unstyled prediction
     wrong (missed live `index.css` import) → owned and explained. HMR observed
     ("auto refreshed without me reloading") and named.
   - [x] **1.4 First commits + push.** ✅ 2026-08-01 — repo
     `Allen1303/first-crack-site` created + pushed via `gh repo create --source=.
     --push` (his call to use the CLI). Read the push output: "it sent the commits
     not the files, gitignore keeps node_modules out." Safety-net commit habit
     started in 1.2 detour.
   - [x] **1.5 Production build.** ✅ 2026-08-01 — predicted JSX compilation ✓,
     size ✗ (guessed node_modules-scale; actual 191 KB → explained the gap: "the
     react and react dom engine code"). Read the build output: empty CSS proves the
     sweep, fingerprinted filenames, gzip column, `public/` copied verbatim,
     `dist/` gitignored.
   - [x] **1.6 Deploy pipeline.** ✅ 2026-08-01 — SECTION 1 COMPLETE. `deploy.yml`
     typed from a filled reference (tap-out invoked; retyped, not pasted), `base`
     added to vite.config, Pages enabled via `gh api` (my wrong `build_type=actions`
     → he read the 422 and we fixed to `workflow`). Green run, live at
     https://allen1303.github.io/first-crack-site/. Exit quiz: first essay attempt
     still fuzzy ("github watch") → re-taught → micro-quiz 5/5 (whose machine, what
     starts it, what document, what folder, runs-every-push). `npm ci` explained.
     **Checkpoint passed:** deleted `src/main.jsx`, rebuilt from blank unaided
     (claims no reference; matched original incl. StrictMode), verified by render.

2. **Design system and static skeleton.**
   Tailwind v4 + the demo's tokens in `@theme`; `stamp`/`display-head` utilities;
   `copy.js`; semantic HTML; Landing, Worth, Footer built for real.
   **Deliverable:** styled, readable one-page site — no interactivity — live.

3. **First real React state: Header and CtaBar.**
   `useState` menu; `useEffect` + scroll listener + `IntersectionObserver` for the
   CTA bar in `App`.
   **Deliverable:** working nav (desktop + phone menu); CTA bar appears mid-page,
   yields to the order section.

4. **The order form (demo mode).**
   Validation with inline errors, radio groups, busy/success states, `localStorage`
   persistence behind the `ORDER_ENDPOINT` seam.
   **Deliverable:** reserve a bag, reload, show the order persisted in DevTools —
   and say out loud why the roaster still can't see it.

5. **The Bloom.**
   Pointer + keyboard events, `requestAnimationFrame` hold-to-fill with settle-back,
   reduced-motion fallback.
   **Deliverable:** press-and-hold ink bloom, releasable, accessible.

6. **The scroll-film engine (the boss fight).**
   900vh track + sticky viewport; scroll → clip index + timestamp; `currentTime`
   scrubbing with lerp-vs-snap; seam-timed captions; preload-2/fetch-ahead loading.
   Whole-file-from-spec.
   **Deliverable:** the six-clip continuous shot scrubbed by scroll, live.

7. **Resilience and accessibility pass.**
   Still-keyframe fallback (reduced motion, Save-Data, video error); keyboard/ARIA/
   focus audit; phone + seam QA with the demo's harness pages.
   **Deliverable:** site fully works with videos disabled and reduced motion on.

8. **The backend: reference, then rebuild.**
   Just before this section, Claude builds the missing layer as a small reference —
   one resource (`orders`), one table, one deploy (Express + SQLite on Render), under
   the same rules as `demo/`: read-only, not shown until I've attempted. I learn the
   API contract (the agreed request/response shapes), rebuild the server myself,
   deploy it, and point `ORDER_ENDPOINT` at it.
   **Deliverable:** reserve a bag on my phone; the order appears in the database and
   is visible from my laptop — the localStorage limitation, actually fixed.

9. **Ship and explain (capstone).**
   Production build inspection, final deploys (Pages + Render), then
   `learning/architecture.md`: my own end-to-end explanation — browser → React →
   scroll math → fetch → Express → SQLite → back, and push → Actions → live.
   **Deliverable:** finished site + backend live, plus my written walkthrough a
   session can fact-check against the code.

## Outstanding understanding checks

- One carried forward: at the end of Section 1, after the pipeline exists, explain
  push → live in five steps (push event → Actions workflow triggers → fresh machine
  installs + builds → output uploaded to Pages → Pages serves the new files).
  Everything else locked 2026-08-01 — see the ✅ notes on each decision.
