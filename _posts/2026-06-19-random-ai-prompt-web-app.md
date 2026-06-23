---
title: "Random AI Prompt: a new home for the web app"
subtitle: "The React front end is reworked into a proper app — matched to the original's look, then decluttered into a focused workspace."
date: 2026-06-19
tags: [random-ai-prompt, update]
---

With [Random AI Prompt](https://github.com/junebug12851/random-ai-prompt)
modernised and documented, attention turned to its React web app, which felt clunky
and incomplete — a light default theme, a cramped column, and most of its features
hidden behind comments so only a bare "Build" tab showed.

The first pass rebuilt the home page to match the look the original pre-revival
generator had established: a dark charcoal canvas, a mint-green accent, pill inputs
and rounded buttons, and the composer and building blocks surfaced together. The
real source files were rebuilt rather than mocked up, and the shared-link feature
that seeds the app from a URL was preserved.

A round of owner feedback then pushed it from "redesigned" toward "feels like an
app." The made-up tagline and centred hero were dropped, the display font was changed
to one that read less like a logo, and image generation, the chaos control, and
presets were removed from the home screen for now — everything pulled out was tracked
in a "removed, pending re-add" note so nothing is lost, with presets explicitly slated
to return later as a richer feature. The layout became a full-height app window with a
title bar and a left building-blocks pane beside the composer, and the prompt input
was simplified so its rotating placeholder *is* the live suggestion.

One process note worth recording came out of the day: an offhand remark that the Share
link "doesn't work and was complicated" was wrongly taken as an instruction to remove
it. It was an observation, not an order; the feature was restored and then actually
fixed and improved — the link now stays visible in a selectable field with a copy
button, so it works even when the clipboard API is blocked. The lesson, noted for next
time, is that a critique is an invitation to explain or ask, not permission to delete.
