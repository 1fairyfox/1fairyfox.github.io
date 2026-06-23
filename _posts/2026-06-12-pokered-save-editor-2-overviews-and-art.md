---
title: "Pokered Save Editor 2: at-a-glance overviews and new badge art"
subtitle: "A Pokémon overview drawer, in-game name rendering in the grid, and a pass to make badge artwork render uniformly."
date: 2026-06-12
tags: [pokered-save-editor-2, update]
---

This day in
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
brought the "View All" overview pattern to the Pokémon screen and tidied up how
artwork renders.

The Pokémon overview is a slide-in table: rows are species (alphabetised), columns
are the party first and then only the non-empty boxes, and each cell shows how many
of that species live there. Hovering a cell lists the differing nicknames and splits
caught versus traded. The view has zebra striping, a sort control that cycles the
same orders as the Pokédex screen, and proper rendering of the gender symbols in
species names — which exposed and fixed a related bug where the box grid showed the
raw `<m>`/`<f>` markers for un-nicknamed Pokémon instead of the ♂/♀ glyphs.

The box screen's "Boxes Setup" control became a Tools menu, and toggling whether the
PC boxes are formatted now opens a direction-aware confirmation: formatting warns
that all but the current box are erased, and unformatting warns that the freed space
can later be overwritten and lost. Proceeding flips a single bit — the engine already
mirrors the game's own load/save behaviour from that bit, so no extra save bytes are
touched.

The rest of the day was artwork. The eight gym badges were full-bleed images with
different aspect ratios, so they each filled their cell to a different width. Each was
re-processed onto a uniform square canvas with the content centred, and the gym-leader
"not yet earned" shadows were recropped to matching square busts. Earned badges now
show the badge icon and unearned ones show the leader's shadow, all at the same
footprint. The trainer and rival card artwork was also swapped to new coloured
illustrations.
