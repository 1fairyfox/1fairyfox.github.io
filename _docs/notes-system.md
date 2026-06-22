---
title: The living-notes system
nav_title: Notes system
category: standards
order: 3
summary: A structured notes/ tree that keeps each repository self-documenting.
---

Every repository keeps a structured `notes/` directory so that anyone opening it —
including an AI assistant working without prior context — can orient quickly. The
canonical machine copy of this standard is in the repository at
`hub/standards/notes-system.md`, with a ready-to-copy skeleton in
`hub/templates/notes-skeleton/`.

## Structure

| Path | Purpose |
|------|---------|
| `status.md` | Current state only — health, what's in flight, what's next. The starting point. |
| `sessions/` | The history: one file per working day (`YYYY-MM/YYYY-MM-DD.md`). |
| `version.md` + `version/` | The changelog — one plain-English entry per commit. |
| `context/` | Background that changes rarely: project, architecture, principles. |
| `systems/` | The system map. |
| `reference/` | Quick-lookup material with no narrative. |
| `decisions/` | Choices made and choices rejected. |
| `plans/` | What's next. |

## The inline-changelog rule

Each changelog entry is written **inside the commit it describes**, not in a
later commit. This avoids a recursion the older "document the previous commits"
approach created, where the documentation commit itself needed documenting.
Because a commit cannot contain its own hash, inline entries carry no hash marker;
`git blame` locates the commit instead.

## A living document

The notes are updated as work happens, by default — not on request. Each kind of
information has one home and one trigger, and the structure is meant to grow:
when something does not fit an existing file, a new file is added in the right
place rather than forcing it somewhere it does not belong.
