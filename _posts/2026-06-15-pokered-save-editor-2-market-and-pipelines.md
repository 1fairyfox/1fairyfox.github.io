---
title: "Pokered Save Editor 2: rebuilding the Market screen, plus screenshots and releases"
subtitle: "The shop screen — long the buggiest in the app — gets a full rework, and the project gains automated screenshots and a release pipeline."
date: 2026-06-15
tags: [pokered-save-editor-2, update]
---

The Pokémart/Game Corner screen in
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
had long been the most half-finished, fragile part of the app. This day was a long,
iterative rebuild of it, plus two pieces of project infrastructure.

**The Market rework.** The screen became a clean two-pane layout: a shopping list on
the left and a cart that reads like a store receipt on the right, itemised with a
running total and balance. Buying and selling were unified into a single cart per
currency, with the receipt summing them into one net total. Mode controls moved out of
the footer into segmented header strips. The standout fix was the money/coins exchange:
the conversion math was inverted, computing roughly twenty coins per ₽1 instead of ₽20
per coin. The game's own data confirmed a coin is worth ₽20, so the data was right and
the code was wrong — and it was reworked into a clear converter with money on one side,
coins on the other, and live deltas. To check this kind of thing against an authority,
the documented Pokémon Red disassembly was cloned in as a read-only reference.

This work also surfaced another use-after-free, traced with a debugger to shop entries
being read from cross-instance static registries after they'd been freed; the fix sweeps
only the current model's live entries.

**An automated screenshot pipeline.** A headless tool now boots the real UI and captures
PNGs of every screen and several states — no manual screen-grabbing, no GPU required for
the fallback path, and it only ever reads the save in memory so it can't touch save data.
Several offscreen-rendering quirks were worked through along the way (missing fonts, blank
grabs, dropped visual effects, and capturing at the app's real window size).

**A release pipeline.** A GitHub Actions workflow now builds release artifacts — Windows
installer and portable, Linux AppImage and tarball, documentation, and screenshots — and
publishes them as a GitHub Release, gated so it only fires when the version was actually
bumped. The first release, `v0.7.2-alpha`, went out with all six artifacts after the
usual first-run shakeout. Screenshots and docs are also served from GitHub Pages so they
stay current without bloating the repository.
