---
title: Research capture
nav_title: Research capture
category: standards
order: 25
summary: If you understood something you didn't understand before, write it down — in the notes, the same session, without being asked.
---

The most perishable thing a project produces is **understanding** — a value's real meaning, what
a routine actually does, a constraint the system can't survive, a field that turns out to be dead.
Code can be rewritten from notes; notes cannot be rewritten from code. So: if you understood
something you didn't understand before, write it down — in `notes/`, in the same session, without
being asked. Distilled from Pokered Save Editor 2's standing rule; general to every project. The
canonical copy is in the repository at `hub/standards/research-capture.md`.

## The shape of a research pass

- **Go to the primary source** — the upstream spec, the reference implementation, the real
  system — not memory, not a previous version, not what a thing is *called*.
- **Verify when it's load-bearing.** If a conclusion is something real will be built on, prove it
  against the actual system (a probe, an emulator or console, a golden output) and commit the
  probe — a careful reading of the source has been wrong before.
- **Write the reference note** — `notes/reference/<topic>.md`: the real names, ranges, who writes
  it, who reads it, what the system does with edge values, and the traps. In plain English, so
  someone who doesn't already know the domain can learn it from the file.
- **Say what it means for the code.** A research pass usually turns up real bugs in the current
  model — list them, and fix them before building anything new on top.

This sits on top of the [living-notes system](/docs/notes-system/) and feeds
[engineering quality](/docs/engineering-quality/) — build on verified understanding, not a guess.
