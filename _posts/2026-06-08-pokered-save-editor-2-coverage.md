---
title: "Pokered Save Editor 2: chasing 90% coverage"
subtitle: "Pushing every library layer past 90% line coverage flushed out a string of real, user-facing bugs."
date: 2026-06-08
tags: [pokered-save-editor-2, update]
---

With a test suite in place,
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
spent a day pushing all three library layers to or above 90% line coverage. The
point of a coverage push isn't the number — it's that writing tests for the
untested paths forces you to read them, and that reading turns up bugs. It did.

A few of the more interesting ones:

- A Pokémon update path was silently dropping the second type of a dual-type
  Pokémon, so editing stats on, say, a Charizard could quietly strip its Flying
  type. The fix scopes the type re-derivation to only run when a type reset was
  actually requested.
- A "minimum EVs" check used "any stat is zero" instead of "all stats are zero,"
  which greyed out the Reset EVs action on heavily-trained Pokémon whenever a single
  stat happened to sit at zero.
- The "is this Pokémon healed?" indicator could never read as healed for any Pokémon
  with fewer than four moves, because an empty move slot was being counted as
  "not at max PP."

Several null-dereference crashes in the map and area code were also fixed, all
behind the not-yet-enabled Maps feature, so they were caught before that feature
ships rather than after.

Two smaller quality-of-life changes landed the same day: item randomisation can no
longer produce a duplicate item within the same list, and the Bag and Pokémon-storage
screens had a round of layout cleanup — the two panes now split evenly through a
proper layout instead of hand-tuned anchors, and stored Pokémon names are always
visible under each icon rather than only on hover.
