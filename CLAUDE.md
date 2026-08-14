# Life-OS App

Phone-first web app front door for Reshma's Life-OS. Spec + decisions live in the
life-os repo: `app-spec.md` (locked 2026-08-13). This repo is the APP CODE only — her
data never lives here.

## Architecture (v1, deliberate)
- **One static page** (`index.html`), no build step, no framework, no server.
- Hosted on **GitHub Pages from this PUBLIC repo** — the shell is public; it renders
  nothing without a token. Her data stays in the private `reshQme/life-os` repo.
- The browser talks **directly to the GitHub API** with a fine-grained PAT she pastes
  once per device (stored in localStorage under `lifeos_token`, scope: life-os repo
  contents R/W only). No token is ever committed here.
- Every write is a **real commit** to life-os: done = line removed from inbox.md/tasks.md
  (or captures/ file deleted) + evidence line appended to log.md. Git is the database.
- Reads are live on every open/refocus — there is no publish step and no cache in the path.

## Rules
- Reshma is a UX designer and art-directs the visuals — build function first, ask
  before imposing styling opinions.
- Never degrade the capture path or Fleet (see life-os CLAUDE.md).
- v1 scope is locked in app-spec.md; do not gold-plate. Sprint/game is a SEPARATE
  design track, not this repo (yet).
- Deploy = push to main (Pages serves the repo root). Test locally by opening
  index.html in a browser.
