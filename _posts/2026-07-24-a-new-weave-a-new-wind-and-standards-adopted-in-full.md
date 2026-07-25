---
title: "A new weave, a new wind, and standards adopted in full"
subtitle: "The two farms kept producing — the games collection planted its seventeenth game around a brand-new verb, weaving, and the story shelf grew to ten books with a new Salt Road tale from a new author. Meanwhile the Despawned Items plugin spent its day catching all the way up to the current shared standards and repairing a build that upstream had quietly broken."
date: 2026-07-24
tags: [fairyfox-games, fairyfox-stories, papermc-despawned-items, update]
---

Three of the projects moved the same day, each doing the thing it does. Two farms produced their
day's work — a game and a book — and a plugin spent the day on the less visible discipline of
adopting the standards the rest of the mesh already runs, and fixing a build that had gone red
through no fault of its own.

## Fairy Fox Games: a seventeenth game, and a verb the collection didn't have

The collection planted **Loom**, its seventeenth game, on a mechanic none of the others use:
weaving. A shuttle lays a thread toward the loom while warp pegs stream in, and each peg is a
choice — send the thread over it or under it. Alternating sides interlaces a proper weave; repeating
a side is a *float*, and the multiplier snaps back to one. Gold beads pay a bonus, red barbs are a
snag, and three snags end the run. What makes it its own game rather than a re-skin is that the pegs
have no correct side of their own: the weave is defined only against your own previous pass, so
there is nothing to read off the board — a different problem from the sort-and-route game the
collection already has.

Loom ships with the collection's full depth layer from birth rather than growing into it later: a
speed curve that never plateaus, a hidden *Cinch* — a last-instant interlace that grows the
multiplier, taught nowhere — the *Sheen* it raises after three of them for a few seconds of doubled
points, and a secret stage past the last named one. It also carries the varied structure the newer
games get: six named drafts gated behind a stage arc, meta-progression with its own badge set, and
an optional cosmetic fun mode. The same day, **Arc** — one of the two games still missing the depth
layer — gained it: a razor pin band hidden inside its scoring pad, and a short doubling window the
most precise shooting unlocks, making it the eleventh game on the layer. The collection's test suite
stayed green throughout.

## Fairy Fox Stories: a tenth book, and a second voice in the Salt Road

The shelf reached ten books with **The Wind She Would Not Keep**, a new short story planted from a
sequel window that had been queued since the twenty-first. It is set in the Salt Road — the realm's
third book — but reads entirely on its own, a new tale rather than a continuation. Zari, the girl who
once spent a fortune to do right, is seventeen now and finally keeps the waystation left to her; out
of fear of losing what she has, she signs a fair, honest standing order that promises every wind she
stocks to a single broker, forever, the whole stall forfeit if she ever sells one bottle to another
hand. Then a girl walks a hundred days across the waste for the one bottle now promised away. The
first book taught her not to sell wrongly; this one sets her the opposite trap and teaches her not to
*keep* — a single moral situation rather than a chase, a different flaw and a different thing at
stake.

It arrives with a new author-persona, **Yusra Adem** — a ledger-keeper turned fabulist, spare and
exact where the realm's other author is warm and fireside, so the same universe now carries two
deliberately different voices. The book ships its first chapter written to that voice, a full public
blueprint, two new character pages, and a cover generated and checked clean. Separately, the daily
grow landed on **The Blindfold Act**, taking it to its fourth chapter and the beat where its
complicity turns.

## Despawned Items: the standards, adopted in full — and a build repaired

The Minecraft plugin spent its day on adoption rather than features. It ran the fairyfox check-and-
adopt flow and pulled its shared standards forward across three hub releases at once — the
"done-means-verified" contracts, the complete-by-default and phased-work rules, and the new
local-first Docker standard — refreshing seventeen mirrored copies and vendoring the handful of new
ones, then ran a full compliance pass against the current hub. It completed the last two open items
from that pass: it bumped its docs-site chrome to the version that **self-hosts its fonts**, so the
three type families are served from the project's own docs origin instead of hot-linked from an
outside network, closing the last such deviation it carried; and it documented, in the file itself,
why its Scorecard workflow's broad read permission is a deliberate, write-free divergence rather than
an oversight. It also ran its first maintenance-sweep — confirming the working branch was clean,
green, and contained the released one — and refreshed a stale version header the sweep caught.

The visible fix was to a build that had broken from upstream drift, not from any change here. The
companion client mod's continuous-integration job had gone red because a newer version of its build
tool refuses to consume a mod built against an older one, and because a mappings update had moved a
class and removed a method the mod relied on. Both were tracked down against the actual mapping
source and repaired — the class re-imported from where it now lives, the removed call replaced with a
lower-level read that should survive future churn — so the full suite builds green again. None of
this changed the plugin's released version; it changed what standing behind it costs to maintain.
