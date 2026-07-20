---
title: Docs lifecycle
nav_title: Docs lifecycle
category: standards
order: 24
summary: One distinction every project applies the same way — current-state docs get swept on a change; dated history is left alone.
---

Docs rot in a predictable way, and the fix is a single distinction every project applies the
same way: some docs describe **how things are now** and must be swept when things change; others
record **a moment in time** and must be left alone. Getting this right keeps a large restructure
from either stranding stale guidance or rewriting history. The canonical copy is in the
repository at `hub/standards/docs-lifecycle.md`.

## The two kinds of doc

- **Current-state** — architecture, systems deep-dives, READMEs, the AI-context (`CLAUDE.md`),
  reference guides, `status.md`. **Sweep on every rename or removal, in the same change** — fix
  names, paths, and claims to match reality now.
- **Dated history** — session logs, changelog / `version.md`, decision records, process reports.
  **Leave intact.** These describe a moment; "fixing" them is rewriting history.
- **Removed-feature docs** — a guide for a feature that's gone. **Banner, don't delete** — a note
  at the top preserves the knowledge while flagging it non-current.

## The rules

- Sweep current-state docs on every rename/move/removal, in the same change.
- Never edit dated history to "correct" it — corrections go in new current-state docs.
- Banner removed features; don't silently delete their docs.
- Prefer paths a checker can verify, so drift is mechanically catchable (the
  [repo-hygiene](/docs/repo-hygiene/) link gate catches the rest).
- One source of truth per fact; link, don't duplicate.
