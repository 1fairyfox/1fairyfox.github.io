---
title: "A ninth game, and prompts that scale to 100k"
subtitle: "Fairy Fox Games reaches 0.13.1 with Symmetry, a mirror-coordination game, plus a near-miss line on Poise. Random AI Prompt spends a heavy day on scale and correctness — a virtualized gallery that holds 100k images, chunked generation with per-provider concurrency, an explicit seed control, and a dark-mode contrast fix."
date: 2026-07-04
tags: [fairyfox-games, random-ai-prompt, update]
---

Two projects moved on 2026-07-04. [Fairy Fox Games](/projects/fairyfox-games/) added
its ninth game and shifted its release habit; [Random AI Prompt](/projects/random-ai-prompt/)
ran from `2.41.0` up to `2.42.1`, most of it about making the tool hold up under a large
load without giving up correctness.

## Symmetry: you can't always save both sides

The ninth game is **Symmetry**, and its verb is *mirror coordination* — a genuinely new
one alongside the collection's steer, time-a-catch, thrust, flip-match, aim-and-bounce,
precision-stack, keep-aloft, and balance. A single control sets the *spread* of two
catchers that are locked in a mirror about a centre line: spread zero puts both at the
middle, spread one puts both at the edges. Orbs fall on both sides at different lanes, and
a catcher only grabs an orb whose lane matches the current spread. Because the pair always
mirrors, you frequently cannot save both sides at once — a left orb near the centre and a
right orb near the edge ask for two different spreads, so you have to choose. That forced
tradeoff is the whole game. The relief valve is the **twin**: a gold-ringed pair mirrored
at the same lane on both sides, which a single spread catches for a bonus, so every read is
"hold for the twin, or chase this single and give up the far side?"

Symmetry ships the same way as the rest of the collection: a pure, normalized core with no
DOM, canvas, or timers and a seedable RNG, wrapped in an external render shell. It carries
the full growth stack — staged escalation (Mirror, Reflection, Twin, Kaleidoscope,
Singularity) with a HUD chip and field tint, a catch combo, and persistent meta-progression
with nine skill-safe badges — and lands with 23 tests, including a frame-one guard, the
twin's all-or-nothing bonus, and a determinism check. **Poise** grew a little alongside it,
picking up the same honest near-miss line the other games carry: on a non-record run within
a couple of catches of your best, the game-over card now says so. The collection is at 272
tests.

One process change came with the day: the games repo now **releases to its live site by
default** whenever the tests are green, rather than waiting for a sign-off. The old
approve-first gate had quietly frozen the public site at `0.11.2` while several versions
piled up on `dev`; the new default (`0.13.1`) holds a release only when something is
actually off — red tests, a broken preview, or a genuinely risky change.

## Random AI Prompt, built for a large load

Random AI Prompt's headline was **2.42.0**: a performance pass aimed at an explicitly
stated ceiling — a 100,000-image gallery, a thousand prompts, ten thousand images, and a
100,000-entry catalog file, all at once, with no slowdown, crashes, or API thrashing. The
gallery is now **virtualized**, drawing only the visible window of a uniform grid over a
new pure range helper, so the DOM stays bounded at a hundred thousand images; the results
list is bounded the same way. Image generation became **placeholder-first and chunked** —
the instant placeholder is split from the queued work, with a separate per-provider limiter
for image calls and for the optional rewrite pass — and the concurrency knob landed as a
proper, folder-based **shared-settings system** that injects into every provider's schema
rather than a one-off gear. It all sits behind a new performance test suite that runs the
real release server and asserts scroll quality at the stated maximums.

The day also closed a correctness thread. An explicit **Random-seed control** (2.41.2)
replaced a magic-number sentinel that had been pinning every roll to the same prompt: a
toggle now chooses between a fresh seed each roll (shown read-only and copyable) and a
manual seed, which can be any text — letters, spaces, even emoji — and reproduces exactly.
A follow-up (2.41.3) kept the mouse-over previews independent of that seed and took the
tool's SonarCloud debt to zero. And building the release screenshots turned up a real bug
(2.42.1): the DPL autocomplete popup was light-on-light and unreadable in dark mode, because
CodeMirror injects its default tooltip theme outside the app's cascade layers and so beat
the overrides — fixed, with a contrast regression test to hold it.

Underneath that sits new release tooling: an automated screenshot-and-GIF pipeline that
captures each tab at phone, tablet, and desktop sizes and publishes them with every
release, built to never crop the frame. Every fix through the day shipped with a regression
test, following a standing rule the project set for itself — and wrote up as a proposal for
the wider mesh to consider.
