# Life-OS App — handoffs

## Session handoffs (newest first)

### 2026-10-19 12:00 — Life-OS App · Yours view (tap-to-done to-do list) · done  (session local_2e692580, started by local_64ed9a80)
**Done:** `index.html` v3 — "Yours" tab (opens first) renders her cross-project to-do list from Life-OS/HANDOFF.md; tapping a card's circle rewrites that item's `Status:` line to `✓ done YYYY-MM-DD (tapped in the app)` and commits "To-do: <title> done (app)" to reshQme/life-os main; second tap restores the old text. Commit fd13552 on main, pushed — **live ✓** once the Pages build passes (see chat / check `gh api repos/reshQme/life-os-app/pages/builds/latest`). CLAUDE.md documents the convention.
**Decided:** no new pages — two tabs under the existing header, same card/circle language as check-off. App never touches HANDOFF.md outside the one Status text (sweep owns the section). Undo text kept in localStorage per device + in the commit body ("was: Status: …"). "maybe done"/"probably done" statuses render red.
**Open:**
- Reshma (hers): open https://reshqme.github.io/life-os-app/ on the phone, tap one circle, check the commit lands in life-os. Not yet tested against the real repo by anyone.
- Claude (Life-OS repo): the sweep's "Claude builds" bullet "App 'Yours' tab with tap-to-done — in progress" is now done; move it to "✓ Done since the last list" (left to the parent session — this one was told not to edit Life-OS directly).
- Claude (later): the sweep rebuilds the section 5x/day — if it ever rewrites a tapped item's Status back from its own snapshot, the tap is lost. The sweep should read `✓ done … (tapped in the app)` as done.
**Next session prompt:** "In ~/AI/life-os-app read CLAUDE.md (section v3) and index.html's 'Yours' block (search `yours: parsers`). Reshma tested tap-to-done on the live site; fix whatever she reports. Test writes only against a local copy of Life-OS/HANDOFF.md (see the node harness pattern: eval the block between the `yours: parsers` markers)."
