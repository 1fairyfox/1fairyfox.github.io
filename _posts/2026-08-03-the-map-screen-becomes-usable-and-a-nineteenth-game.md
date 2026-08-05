---
title: "The map screen becomes usable, and a nineteenth game"
subtitle: "The save editor's map screen, whose feature work had been landing as plumbing for a week, finally became an editing surface you can actually drive — sortable and searchable, with randomize and revert on every field. The games collection planted its nineteenth game, a genuinely new verb: growing a length to fit a gap you can see."
date: 2026-08-03
tags: [pokered-save-editor-2, fairyfox-games, update]
---

Two projects moved, and both moved a piece that had been groundwork into something a person can use.

## Pokered Save Editor 2: the map screen ships its editing surface

For weeks the save editor's map view has been growing underneath — an emulated overworld, editable
sprites and warps and signs and connections, per-map script progress, all 2,560 world event flags.
What it lacked was the ordinary usability that turns a technical achievement into a tool. This day
supplied it, walking the version from 0.43.6 up to **0.43.21-alpha** across a run of focused changes.

Every editable field on the map screen gained a **randomize** button and a **revert** button — the
latter restoring the last-saved value, the small undo that makes fearless editing possible. The map
selection list became a shared, sortable, searchable control with right-aligned sizes and a "show
unused maps" toggle, so a save's 200-odd maps are navigable rather than a wall. The tileset and
blockset selectors, which had been floating in a designated-maps panel, folded into the
map-selection panel where they belong, with a sync offer when a tileset and its blockset disagree.
Sprites and NPCs now recolour along with the colour filter instead of ignoring it. The window even
opens at its true design size after a doubled-default-size bug was found and corrected. Individually
these are small; together they are the difference between a screen you can demonstrate and a screen
you can work in — the feature the earlier plumbing was always for.

A second cleanup wave followed, to **0.43.22-alpha**, this time on the top bar itself. The single
"show useless edits" toggle became a dropdown of *tiers* of abnormal values — "Unused & unstable"
(values the game reads and acts on but were never meant for play, up to and including crashes) and
"No-effect edits" (overwritten on load, read-only, or simply never read) — with a level light that
shifts grey to blue to red to show which tier is currently revealed; the map list's separate
unused-maps filter folded into that one global switch. The list also gained two more ways to sort —
by semantic size bucket, and grouped by a map's connection signature — with the sort selector moved
up beside the search box, and the tileset and blockset controls gained explicit Separate and Merge
buttons in place of the automatic split.

## Fairy Fox Games: Span, the nineteenth game

The collection planted **Span**, its nineteenth game and a new verb: building, or bridging. You are
not steering, timing, aiming, metering, swinging, remembering, guarding, herding, weaving, sorting,
or resisting — you are growing a length to fit a gap you can see. Your fox stands at a ledge; a gap
yawns ahead, then the next ledge. Hold one control to grow a beam upward, release to drop it flat
across the gap, and the length at the moment of release is its reach. That makes a miss two-sided —
fall short and the tip drops into the gap, grow it too long and it overshoots and you walk off the
far end — which is exactly what makes it its own thing rather than a charge shot or a metered pour.

Like the recent games, it ships with its full depth layer from birth. Landing anywhere crosses, but
a loose landing snaps the multiplier back to one; land on the drawn keystone and it climbs; and
dead through the exact centre — a razor sub-window that is drawn nowhere — is the *plumb*, which pays
a flat bonus and builds a streak, three plumbs in a row lighting a doubling window. Safe play and
greedy play share the one button. A run is a seeded sequence of named crossings — Steady, Reach, The
Bench, Stagger, The Narrows, The Gauntlet — that gate open as the stages climb, and a secret stage
waits past a hundred and ten crossings for anyone who reaches it. The whole thing rides the
collection's usual split: a pure, timer-free core with a real thirty-four-test suite, and a shell
that does nothing but render it.

## The shape of the day

Both projects did the same kind of work in different registers — taking something that already
technically existed and making it usable. The map editor turned an emulated screen into an editing
surface; the games collection turned a new idea into a playable, tested verb. Small, honest outputs;
the useful kind.
