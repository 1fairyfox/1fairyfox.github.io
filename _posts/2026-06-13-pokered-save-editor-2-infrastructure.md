---
title: "Pokered Save Editor 2: versioning, i18n, a Linux test container, and real GUI tests"
subtitle: "A heavy infrastructure day — single-source versioning, translation plumbing, a Dockerised Linux harness, and tests that drive the live app."
date: 2026-06-13
tags: [pokered-save-editor-2, update]
---

A lot of foundation went into
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
this day. None of it is glamorous on its own, but together it's the scaffolding the
rest of the project leans on.

**Versioning.** The version number now lives in one place — a `VERSION` file at the
repo root — which CMake reads and propagates into the runtime, the About screen, and
the Windows executable's resource information, with the git commit appended as build
metadata. There is no longer a hardcoded version anywhere to drift out of date.

**Internationalisation.** UI strings are now wrapped for translation, with per-locale
catalogs compiled and embedded and a translator installed at startup. The source
language is US English and game-data names are deliberately out of scope. Actual
language switching is held until there's a second locale and an options screen to
choose it from; the plumbing is in place.

**A Linux test container.** A Dockerised build-and-test environment mirrors the
development kit and adds what the Windows kit can't run — Address/UB sanitizers — plus
a real virtual display and coverage reporting. On its first run all variants passed,
sanitizers clean, with line coverage just under 90%.

**Tests that drive the real app.** Two new kinds of test were added. One loads every
screen through the real engine and fails on any load error or warning — the kind of
problem the C++ unit tests can't see because they never instantiate the UI, and
exactly what had let a non-opening Credits screen slip through earlier. The other
boots the actual application headless and drives it: navigating every screen, editing
fields through the live UI, saving, reopening, and asserting the changes persisted —
including a byte-fidelity test that browses everything without editing and confirms
not a single save byte changed.

Those tests immediately caught real crashes: a garbage save file crashing on load, the
shop screen aborting when opened with an empty cart, and a badge-count function that
had been stubbed to always return eight. The day closed with an end-to-end redesign of
the Credits/About screen onto a data-driven back end, so adding a credit is now a
single data edit.
