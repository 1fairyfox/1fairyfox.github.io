---
title: "A coin that travels, and a map that reads the evidence"
subtitle: "The hub mints a small shared reading reward and a batch of cross-brand engineering standards — and by the end of the day every project has pulled them in. Pokered Save Editor 2 teaches its map screen to read a save's real progress instead of shrugging at it, writes down the whole game's reset map, and draws a flag's state the instant it changes. Fairy Fox Games gives Skyline depth inside its one verb. Fairy Fox Stories tells the third chapter of its first mystery. Random AI Prompt takes the new coin and standards into its own docs."
date: 2026-07-19
tags: [pokered-save-editor-2, fairyfox-games, fairyfox-stories, random-ai-prompt, site, update]
---

Two things happened at once today. The hub finished a feature it had been building the day
before — a small coin you earn just for reading around the mesh — and wrapped a batch of
engineering standards around it. Then, one after another, every project pulled that same coin
and those same standards into itself, so a thing minted in the morning was everywhere by
night. That is the shape the mesh is meant to have: the hub writes something once, and the
projects adopt it on their own, on request, without anything reaching across a wall to force
it. The other headline is smaller in scope and larger in craft: Pokered Save Editor 2 spent
the day teaching its map screen to read the evidence a save actually carries.

## fairyfox.io: a coin for reading, and the standards around it

The coin is deliberately quiet. Open a page you haven't read today — anywhere under the
fairyfox.io domain — and a small counter beside the reader button ticks up by one. The balance
is shared across every project's site in the same browser, and reading a longer page to the end
pays a little extra. It is a garnish, never a gate: everything on every site is fully available
to someone with zero coins, and the standard that governs it spends most of its words insisting
on restraint. A plain-language page at `/legal/coins/` explains exactly how it works and what it
does and doesn't store, and the hub finally serves its own Privacy, Terms and Cookies pages
alongside it, which it had been missing.

The coin arrived carried by standards, because a shared feature is only shared if every project
holds to the same rules about it. A deep read of the siblings' own working notes turned up nine
conventions worth making mesh-wide — testing, engineering quality, repo hygiene, the
current-state-versus-history docs rule, research capture, the working rhythm an agent keeps, a
no-third-party-assets rule for published sites, and the operating model the two farms share —
each written once, each with a concrete check, each wired into the single compliance audit. A
later pass in the day folded in one more, a maintenance-sweep procedure proposed by Random AI
Prompt after a real sweep found a status page five versions stale. The site's own documentation
library now carries a readable page for each of these standards, so the list on the site matches
the rules the code actually follows.

## The mesh adopts it, the same day

What makes the day worth recording is that the adoption did not wait. Random AI Prompt pulled
the new coin counter into its documentation chrome and took six of the new standards in as
reference notes — no change to the prompt engine itself, just its docs learning the same
vocabulary. Fairy Fox Games adopted the standards text as the first phase of the coin rollout,
vendoring ten new reference notes and refreshing the ones that changed. Fairy Fox Stories did
the same, took the release-by-default posture and wired in the broken-link and tidy gates the
repo-hygiene standard asks for, and deliberately *deferred* the visible coin work to a later
session with a browser attached — because a rule the mesh now shares says a UI change may not
ship unseen. Pokered Save Editor 2 replaced its hand-built documentation chrome with the hub's
vendored bundle wholesale, keeping only a self-hosted-fonts deviation it filed back as a
suggestion. Four projects, one source, one day.

## Pokered Save Editor 2: a map that reads the evidence

The feature work was about a stubborn question — where in the game is this save? — and the map
screen used to answer it badly. When a save sat between the researched story stages it showed a
"Custom (matches no researched state)" row and gave up. Now it does its best instead: it scores
every resting stage against the flags a stage is known to flip, the map's own missable objects,
and the progression byte, and picks the closest, so a played save's Pallet Town reads "Oak has
led you to the lab" rather than "custom". Every raw step the game's own script table can hold is
in the list too, as italic entries, so choosing a state covers everything the byte can legally
be.

Underneath that is a large piece of research written down in full: the whole game's progression
graph. Of the 2,560 event flags only seventy are ever reset — progress is almost entirely
one-way — and the exceptions fall into five named classes, the surprising one being maps that
re-arm *other* maps' puzzles every time you enter them. Beating Giovanni at Silph hides
thirty-four objects across eleven maps in a single sweep. All eight badges are provably
mandatory. With that map drawn, the editor can now recognise a bit that looks wrong as a
mid-cutscene save rather than corruption. The visible payoff came last: all 228 of the game's
filter flags gained researched lifecycles — what each is, its default, and every script that
shows or hides it — and the map canvas now redraws a flag the moment it changes, so flipping
Professor Oak's street cameo fades him between drawn and ghost right there instead of on the
next reload.

There was also a quieter, wider change: a pass that took the project's notes and instructions
into a neutral, professional voice — dropping decorative emoji and combat metaphors, and
rephrasing first-person ownership as role-based project leadership — the same documentation
discipline the site itself keeps.

## Fairy Fox Games: Skyline gets depth inside its one verb

Skyline was the oldest game in the collection still missing the "depth inside the mechanic"
layer, and it carried exactly the plateau that layer exists to fix: its fall speed climbed to a
hard cap early and then sat flat forever. All four additions land on the one drop verb and are
safe to never notice. Setting a slab flush to the *pixel* — a razor window hidden inside the
ordinary flush window — pays a Keystone bonus and builds a streak; three Keystones in a row open
a Jet Stream where the next few drops score double; the speed curve became a smooth asymptote
that keeps climbing past where the old ramp died; and a secret Exosphere stage waits past the
visible end, revealed only by reaching it. It is the seventh of the older games to gain the
layer.

## Fairy Fox Stories: the third chapter of the first mystery

The story farm grew its daily chapter, and the blend that picks which book to advance ran clean
— no random override this run — landing on *The Blindfold Act*, the shelf's first mystery, which
had the most unfinished plan and had gone stale, exactly as the previous day's note predicted it
would. Chapter three, "The Tells", turns the screw on a cold-reading fraud who clears a
suspect publicly at the cost of exposing his own trick — "his debts are his alibi" — and ends on
a mercy she pointedly refuses to extend a second time. The book is halfway through its planned
six chapters.
