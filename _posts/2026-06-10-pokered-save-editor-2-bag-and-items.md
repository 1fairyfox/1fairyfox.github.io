---
title: "Pokered Save Editor 2: bag drag-and-drop and careful item handling"
subtitle: "The items list gets the same drag interactions as the box grid, plus auto-stacking that never loses an item."
date: 2026-06-10
tags: [pokered-save-editor-2, update]
---

The drag interactions added to the Pokémon box grid came to the items list this day
in [Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2).
You can reorder items within a list and transfer them between the Bag and PC storage
by dragging a left grip handle — the handle exists so the row's own quantity and
selection controls keep their clicks. The bulk-action footer was dropped here too,
replaced by per-row delete chips and group actions through the checkboxes.

The interesting design work was making transfers safe. When you drag an item onto a
matching item, it auto-stacks — but only when the whole amount fits under the
game's per-slot cap of 99. If it would overflow, it becomes its own second row with
the full amount kept; if there's no room even for that, the transfer is refused and
the item stays put. The rule throughout is that a transfer never clamps or silently
drops items. The item dropdown also greys out items already present in the same pane
and shows the total owned across both panes next to each name.

A new "View All" overview drawer was added to the bag: a slide-in panel with a
condensed, alphabetised table of every item the save holds and its counts in the Bag
and in storage. It started as a standard drawer component, but that left a stubborn
white frame, so it was rebuilt as a hand-rolled slide-in panel for full control.

One smaller item: the in-app Credits screen is now treated as a living document,
kept current as the project changes rather than updated after the fact, and it now
acknowledges the development tooling used in the 2026 revival.
