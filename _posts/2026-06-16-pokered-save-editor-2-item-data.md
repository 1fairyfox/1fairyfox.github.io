---
title: "Pokered Save Editor 2: grounding item data in the game's own source"
subtitle: "Splitting the shop's item groups using the original game's disassembly as the authority, plus accented names and detailed tooltips."
date: 2026-06-16
tags: [pokered-save-editor-2, update]
---

A theme running through
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
is that claims about the game should be checked against the game, not guessed. This
day put that into practice on item data.

The Market's flat "Normal Items" list was split into meaningful groups, with the
documented Pokémon Red disassembly as the oracle. The buyable set is the union of
every reachable in-game shop's stock; items with no price at all in any currency are
listed nowhere, because there's genuinely no way to buy or sell them. After a couple
of corrections — the vending-machine drinks really are buyable in-game, just from a
separate vendor, and every priced item is in fact buyable and sellable *in the
editor* regardless of how the real game treats it — the grouping settled into Normal
Items, Vending Machine, and Special Items, each backed by index sets transcribed
directly from the disassembly's data files. The Sell list was also tightened to hide
only items that truly can't be sold while keeping free ones.

Two more changes landed. A display-wide sweep corrected "Poke" to the accented "Poké"
everywhere user-visible — Poké Mart, Poké Ball, Pokédex — touching only display
strings, never internal identifiers. That sweep tripped a subtle trap: one item name
doubles as a lookup key in the map data, so renaming it orphaned a link until the data
reference was updated to match; a reminder that display text and data keys aren't
always separable. The editor's target was also documented explicitly as the US English
release of Red and Blue.

Finally, the long-deferred detailed item tooltip feature was built as a working
vertical slice: an optional info field per item, plumbed through to a tooltip with a
title and wrapped body, with the first eleven items' descriptions authored and checked
against the disassembly. The rest of the items, and wiring the tooltip into the other
screens, are the next steps.
