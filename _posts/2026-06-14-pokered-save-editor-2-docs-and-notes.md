---
title: "Pokered Save Editor 2: tightening the docs and notes system"
subtitle: "Standing policies for versioning and docs, a structured documentation site, and a deep cleanup of the project's living notes."
date: 2026-06-14
tags: [pokered-save-editor-2, update]
---

This was a maintenance-and-discipline day for
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2) —
the sort of work that keeps a project legible as it grows.

Two standing policies were adopted. The version number is now kept current as part of
each change rather than in a separate bump later: patch and minor increments are applied
in the same commit as the work, while a major version is reserved as a deliberate,
owner-only decision. And the generated API documentation is rebuilt by default whenever
the stable branch advances, so the published docs always track what's released.

The documentation site itself was reorganised from an auto-appended pile into a
structured tree, with the project's notes built in as a proper navigable hierarchy
alongside the C++ API reference. A hard rule came out of it: every documentation page
has to be explicitly placed in the navigation, or it floats loose — so placement is now
part of adding a page.

The bulk of the day was a deep overhaul of the project's living-notes system. Per-day
session logs replaced a single growing log file, dated history was moved out of the
current-status page so that page describes only the present state, and several
overlapping reference documents were consolidated. The notes had also briefly swapped
real names for a generic "the maintainer" everywhere; that was reverted to plain names
used only where attribution matters, in neutral phrasing.

This kind of change doesn't move the version number — documenting the documentation is
exactly the noise the inline-changelog policy is designed to avoid — but it's recorded
here because the notes are how anyone, human or otherwise, gets oriented in the project
cold.
