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

## Storage conventions written by the app (v2, 2026-08-19)
Both live in the markdown, not localStorage — git stays the database and the static
pages/builders can read them.

- **Priority star:** the item line begins with `★ ` after its bullet, e.g.
  `- ★ Order contact lenses` or `- [ ] ★ Ch 1–25 revision`. Starred items float to the
  top of their section. **`keyOf()` in build-today-html.js strips a leading ★ before
  keying `.ages.json`** — starring must never reset an item's age (ages are load-bearing).
  If you touch either builder copy, keep that strip in place (viewer + `life-os/tools/`).
- **Today tray:** a `## Committed` section in `today.md`, ordered `- item` lines. The app
  writes it on commit / uncommit / reorder. Inserted just above `## Plan` if absent.

## v2 features (2026-08-19)
- ★ stars, ⬇ Today tray, drag-to-commit AND tap `↑ Commit` (pointer events — one code
  path for mouse and touch; drag out of the tray = uncommit).
- `📥 last capture received` line under the header — reads the newest `Back tap` commit
  touching `captures/`, so it works even when the folder is empty. Turns red past 48h.
  This exists because three separate silent capture failures happened on 8/19 alone.
- **✨ Claude triage** — on-demand only. Anthropic key in localStorage (`lifeos_anthropic_key`),
  called direct from the browser with `anthropic-dangerous-direct-browser-access`.
  Model `claude-sonnet-5`. It ONLY returns suggestions and never writes a file — a 401
  clears the stored key so she can re-enter it.
- Finishing a task fuzzy-matches its **inbox twin** and offers to remove it (always
  confirmed — a wrong match would destroy a capture).
