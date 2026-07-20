---
title: Testing and verification
nav_title: Testing
category: standards
order: 21
summary: Every project proves its work — real, layered tests that run before shipping, and a visual change previewed with human eyes first.
---

Every mesh project **proves** its work rather than merely making it look right. Tests are real,
layered, and run before shipping; a visual change is previewed with human eyes first. This
distils the practice the projects already share — the games' pure-core split, Pokered Save
Editor 2's console/emulator oracle, Random AI Prompt's two-gate isomorphic verify. The
canonical copy is in the repository at `hub/standards/testing.md`; it says *what* verification
is owed, not which framework to use.

## The rules

- **Split pure logic from rendering.** The core logic lives in pure modules — plain data and
  pure functions, no DOM, canvas, timers, or I/O — and the shell does rendering, input, and the
  loop. This is what lets a thing be *proven* to work instead of *looking* like it works.
- **Real, multi-layer tests — not token ones.** Cover the layers that can actually break: math
  and data, state transitions, boundaries, success/failure paths, and integration where units
  meet. One or two cheap asserts is not coverage.
- **A bug fix ships with its failing-case test.** Every fixed defect lands, in the same change,
  with a test that fails on the old behaviour and passes on the fix — demonstrated fail-then-pass,
  in the right home (logic bugs in the unit suite, UI/z-order bugs in the end-to-end lane written
  functionally). This is the single highest-leverage test a project writes.
- **Run the gate before shipping; only proceed on green.** Where code runs in more than one
  runtime, verify each — one gate isn't enough.
- **Preview visual changes with human eyes.** A UI change is looked at before it ships; it may
  not go out unseen.
