---
title: "Pokered Save Editor 2: a redesigned Pokémon editor"
subtitle: "The General, DV/EV, and Moves tabs are rebuilt into one visual language — and a long-standing display bug that showed the wrong types is fixed."
date: 2026-06-17
tags: [pokered-save-editor-2, update]
---

The Pokémon detail editor in
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
was the last major area still carrying its 2020-era layout. This day brought all
three of its tabs — General, DV/EV, and Moves — up to the same visual language the
rest of the app had settled into: grouped panels of zebra-striped rows, connected
segmented controls instead of loose buttons and overflow menus, and consistent
sizing.

The General-tab redesign ended on a real, long-standing bug. The type dropdowns had
been displaying the wrong type for every Pokémon — Charizard reading as
Ghost/Fighting instead of Fire/Flying — and "reset to default" appeared to do
nothing. A diagnostic test proved the underlying data was correct all along; the
combos just rendered it wrong, because of an off-by-one between the type list's
"no type" placeholder row and the stored type index. It was a one-line fix, now
guarded by tests that assert the real type IDs rather than comparing a value to
itself.

The DV/EV tab gained segmented DV/EV switching and a "Future Shiny" control whose
selection is bound directly to the data, so dragging the DV sliders into a shiny
combination flips the indicator on its own — one source of truth, no drift. The
Moves tab was reworked into draggable, reorderable rows with a clean PP / PP-Ups
view toggle; an in-app review caught it rendering empty at first, which turned out to
be three separate UI bugs (a zero-width layout, an id collision, and a model rebuild
race) all worth documenting.

The day finished with a data-integrity pass: destructive actions in the editor —
re-roll, reset, max out, evolve, and the bulk move operations — now ask for
confirmation through a shared dialog, while harmless per-field actions don't. A
status badge was added to the Pokémon preview, and the level field was widened so
"100" fits.
