---
title: Engineering quality
nav_title: Engineering quality
category: standards
order: 22
summary: The standing quality bar every project holds to — clean, correct, finished work, documented and tested, with no rough-in left for "later".
---

The mesh's standing quality bar. Every project — a save editor, a prompt engine, a games farm,
a story farm — holds to the same floor: clean, correct, finished work, documented and tested,
with no rough-in left for "later". This makes shared and checkable the value the projects state
in their own words ("no hacks, no temporary fixes"; "do the long work"). The canonical copy is
in the repository at `hub/standards/engineering-quality.md`; its companion is
[testing](/docs/testing/) (proof) — this one is the bar the work is held to.

## The rules

- **No hacks, no temporary fixes, no bad fallbacks.** Prefer the correct, clean solution even
  when it's the longer route. If the only path you can see is hacky, surface it and ask — a
  silent workaround is worse than a stated blocker.
- **Do the long work — no rough-in.** Big features are built as phases, one finished body of
  work at a time. A phase that is 90% done is not done.
- **Best craftsmanship, always — proportionate, never absent.** From the smallest utility to
  the largest system, the work is genuinely well made.
- **Clean, modern, modular, focused code.** Small focused units, clear boundaries, no needless
  duplication, current idioms for the stack.
- **Full documentation and doc-comments.** Public surfaces carry doc-comments; the docs explain
  how the project is built and used, kept current.
- **Fearless refactoring, behind the test gate.** Improve structure whenever it pays — and
  update the tests with it. The green suite is what makes a refactor safe.
- **Fidelity to the source of truth.** Where a project stewards someone's data or a real format,
  change only what the task requires and leave the rest exactly as it was.
