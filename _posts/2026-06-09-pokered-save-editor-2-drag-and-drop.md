---
title: "Pokered Save Editor 2: drag-and-drop box management"
subtitle: "Storage boxes get drag-to-reorder and cross-pane transfer — and an intermittent crash gets traced to its real cause."
date: 2026-06-09
tags: [pokered-save-editor-2, update]
---

Pokémon storage in
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
now supports dragging. You can reorder Pokémon within a box and drag them between
the two visible panes, with an insertion caret showing where a drop will land and a
small drag threshold so a plain click still opens the editor. Group moves work
through the existing checkboxes, and each cell gained a per-item delete chip with
proper hover and press states. The bulk-action footer bar was removed in favour of
these direct interactions.

The more instructive part of the day was an intermittent crash: create or open a
stored Pokémon's editor, back out, reopen, and the app would occasionally crash on a
freed object. The first fix attempt addressed ownership of the individual Pokémon
and didn't hold. The real cause turned out to be one level up — the *box*, not the
Pokémon. A box object was being handed to the UI layer's garbage collector, and when
it was collected it deleted every Pokémon inside it, leaving them dangling no matter
how their own lifetime was managed.

The fix makes boxes and the objects they contain declare C++ ownership from
construction, so the UI engine never assumes it can free them. Containers still
release their contents normally, so there's no leak — the objects are simply
protected from being collected out from under the application.

A worthwhile footnote came out of the debugging: two of the retests "failed" only
because they were run against a stale built library in a different output directory
than the automated tests use. The lesson, now written down, is to verify the build
you're actually running by timestamp, not by assumption.
