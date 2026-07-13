---
title: "A Game Boy inside the editor, and a real phone under the app"
subtitle: "Pokered Save Editor 2 stops drawing pictures of maps and starts emulating them — then builds a Game Boy sound chip in C++ and lets the cartridge grade it, frame by frame. Random AI Prompt puts its Android build on a real device and finds the defect was its own test. Fairy Fox Games plants Brim, a game about the water still in the air."
date: 2026-07-12
tags: [pokered-save-editor-2, random-ai-prompt, fairyfox-games, fairyfox-stories, site, update]
---

The theme of 2026-07-12 was **the oracle** — the discipline of asking something outside
yourself whether you are right, and being willing to hear no.

Pokered Save Editor 2 spent the day handing its work to an actual Pokémon Red cartridge,
running in an emulator, and asking it to check the answers. Random AI Prompt put its Android
build on a real Android runtime rather than trusting a claim it had been making for weeks.
Both were told they were wrong about things they were confident about — and in both cases the
wrongness was in the *instrument*, not only in the code.

## Pokered Save Editor 2: the map, actually emulated

The editor's map screen has always drawn a *picture* of the map. Today it stopped doing that
and started running the game's own overworld pipeline: the blocks, `wOverworldMap`,
`wSurroundingTiles`, `wTileMap` — the arrays the console itself builds, in the order it builds
them (`0.17.0`).

Which raises the obvious question: how would you know if it were wrong? So the project built
an oracle (`0.18.0`). A legally backed-up cartridge, never committed and refused by
`.gitignore` anywhere in the tree, is booted **headless in PyBoy** with the editor's own save
fixtures. The emulator loads the save, and the harness dumps what the *game* actually did — the
view pointer it computed, its overworld buffer, its scratch area, its on-screen tilemap. A test
then demands the editor match it byte for byte.

The first run matched on four of five arrays and **failed on the fifth**, exactly as suspected:
the three-block border ring. The editor filled it with the map's border block. The console does
that *and then bleeds the neighbouring maps' edges over the top* — Pallet Town's ring is really
Route 1's bottom rows and Route 21's top rows, which is why you can see up the route before you
walk it, and why the walk across is seamless. It was held as an explicit expected failure rather
than skipped, so it could not be quietly forgotten.

**Connection strips closed it** (`0.19.0`). They are notoriously fiddly — the length byte means
a *width* going north/south and a *row count* going east/west; a negative offset slides the
*source* rather than the destination; 66 of the 78 connections in the game read across a bank
boundary. All of it was re-derived from the game's own `connection` macro, and then checked: a
script finds every map header in the ROM by signature and compares all eleven compiled bytes
against the editor's recomputation. **78 of 78, zero mismatches.** The expected-failure marker
was deleted.

The same discipline turned up something better than a fix.

**The six glitch palettes are real** (`0.20.0`). The save byte the app calls "contrast" is
`wMapPalOffset`, and the game does something unsafe with it: it *subtracts* the byte from a
pointer into a table of eight contiguous three-byte fade palettes. Land on a multiple of three
and you get one of the four real contrast levels. Land anywhere else and the read straddles two
entries and produces three bytes that are not a palette anywhere in the game — six of them,
exactly. Not simulated, not approximated: the editor applies the byte the console would
genuinely be holding, so the glitch palettes come out as the real article. Ten values written
into saves, ten booted on the cartridge, ten palette registers read back: **10 of 10.**

Then the player was drawn (`0.21.0`) — and the two palettes that had looked *harmless* stopped
being harmless, because their damage is to the object palettes, and now there is an object on
screen. The map stays perfectly normal and the player alone goes wrong. That is what a Game Boy
does with that byte.

Three sprite facts were pinned along the way, each of which would have been got wrong by
guessing: there is **no right-facing sprite** (facing right is facing left, X-flipped); there is
**no second walking frame** (the four-state walk is one drawing, mirrored); and sprites sit four
pixels *above* their tile row — confirmed twice, from the disassembly's own comment and from the
console's OAM.

## Pokered Save Editor 2: 151 pieces of music, and not one audio file

The map screen now plays the game's soundtrack, and there is not a single audio file in the
repository.

The music is assembled straight out of the `pret/pokered` disassembly by an importer that
proves itself twice (`0.22.0`): a track's id is *computed from its header's address*, so the
importer recomputes all 46 ids from the table it just built and refuses to write anything if one
disagrees; and, with the cartridge present, it walks its own byte stream and the ROM's in
lockstep, command by command. **All three banks match the cartridge.** 38 KB, and it is the whole
soundtrack.

Playing it required a Game Boy. So the project wrote one: `pse-audio`, holding a **DMG APU
model** — four channels, the 512 Hz frame sequencer, envelopes, sweep, the LFSR, wave RAM, DAC
semantics — and a **transliteration of Gen 1's sound engine**, whose entire state is a 256-byte
array laid out exactly like the console's `$C000`. The seam between them is the design: the
engine emits register writes and knows nothing about sound; the chip knows nothing about notes.

Which is what makes the oracle possible. `tst_sound_parity` boots the real cartridge with a track
patched into a save, photographs the engine's 256 bytes of state **on every frame**, and requires
the C++ port to reproduce every one of them. **All 46 tracks, plus an inner voice, byte for byte,
frame by frame** (`0.22.1`).

It earned its keep on the first run, and the findings are a good illustration of what a real
oracle is for. Three were bugs of *tidiness* — places where the port had helpfully done the right
thing and the game does the wrong one. `InitPitchSlideVars` clobbers a register the caller only
saves afterwards, so a pitch-slide note starts on a divide's **leftovers**, not on its pitch; the
port had kept the correct pitch, and was therefore wrong. `PlaySound` never restores the current
sound id, so after a drum the engine's "current sound" *is* the noise instrument; the port had
saved and restored it, inventing a hygiene the game does not have. It is not a bug to fix, it is
a bug to copy.

The fourth finding was the most valuable: **the oracle itself was wrong.** Entering a map fades
the old music out first, and during the fade the channel ids already read as the *new* track while
the audio bank register still holds the *old* bank — so the command pointers being photographed are
addresses in a different bank's data. It produces a dump that looks entirely plausible and is
complete nonsense, and half the tracks "failed" against it. A wrong oracle is worse than no
oracle, and this one was wrong in a way that reads as an engine bug.

And the glitch music turned out not to exist. A song's id is derived from its header's address, and
a header is three bytes *per channel* — so a three-channel song occupies three consecutive ids, and
the other two parse perfectly well as one-channel headers pointing at that song's channel-2 and
channel-3 streams. **Id 186 is Pallet Town. Id 187 is Pallet Town's bassline, alone.** All 256 ids
across three banks were parsed out of the cartridge: 46 real tracks, **105 inner voices, and zero
garbage**. The console was asked to confirm it, and did. The panel now lists all 151, grouped and
named, each inner voice indented under the song it came out of — hover auditions, click commits
(`0.23.0`).

## Pokered Save Editor 2: a bug that put a bedroom's walls in a Poké Mart

Working out what the map *means* — walls, grass, water, warps, ledges, counters — surfaced a save
corrupting bug that had been there since the first version (`0.24.0`).

The collision lists are **shared** in the cartridge: `RedsHouse1_Coll` and `RedsHouse2_Coll` are two
labels on one list, as are Mart/Pokecenter and Dojo/Gym. The original importer assumed one list per
tileset in index order, and walked the chain one step out of phase for three of them. Since the
editor *writes* that pointer into the save, putting the player in a Poké Mart wrote **Red's-house
collision** into their game — wrong walls, wrong door, wrong counter, in the real thing.

Fixed in three lines, and negative-controlled: a test now re-derives every collision pointer from the
list data, so pointers and lists cannot disagree again in either direction. Put the bug back and two
cases fail by name, one of them reading *"A Poke Mart would get a bedroom's walls."*

The day closed with the map **animating** (`0.24.4`) — and writing that loop exposed two more
invented facts. The console does not slide the water tile from 0 to 4 pixels and back; it *rotates*
the sixteen bytes of the tile, swinging from −1 to +3, because the direction flips halfway while the
offset keeps accumulating. And the flowers do not cycle evenly: the first is shown twice as long as
the other two. Both of the old behaviours were plausible. Both were made up. The test now checks that
each water step is a genuine rotation of the tile rather than a second picture of it, *because that is
what the console does — it does not have a second water tile, it rolls the one it has.*

## Random AI Prompt: the promise, measured

The prompt tool has been advertising a number — 1,000 prompts in a roll — and on mobile it had never
actually been checked on a phone. Today it was, and the exercise is a small lesson in instruments.

First the app was put in CI at all (`2.58.0`): a test presses every control rather than merely
rendering it, behind coverage gates. Getting there took a run of failures that were all about the
*harness*, not the app — an emulator launching the app behind its own lock screen, a dark screen
granting window focus to nobody, the launcher itself throwing "app not responding" dialogs on top of
the thing under test.

Then the measurement (`2.60.0`), and for a few hours the notes said the app had **failed** its own
promise: 1,000 prompts, no completion inside a ten-minute timeout. It was wrong. The instrumentation
added to diagnose the failure is what disproved it — the engine produced all 1,000 prompts in 13
seconds on a software-rendered emulator, and React committed every row **34 milliseconds later**. The
bug was in the test: results accumulate across rolls by design, so after a 20-prompt baseline the
label reads "220 generated", and a test waiting for "200 generated" waits forever, then reports its own
timeout as the app being slow.

The real figures, from the release APK on a real Android runtime:

| Roll | engine | render | memory |
|---|---|---|---|
| 20 | 1,497 ms | 383 ms | 112 MB |
| 200 | 5,447 ms | 196 ms | 122 MB |
| 1,000 | 23,366 ms | **253 ms** | **110 MB** |

Fifty times the rows, for no more memory and no more render time. The list virtualizes exactly as
claimed — and now it is a measurement rather than a claim.

## Random AI Prompt: a filename that could run a program

CodeQL flagged it on the release PR and it was right (`2.60.1`). Two backend routes built a **shell
string** around a request-derived file path to open an image or reveal it in the file manager. Path
traversal was blocked; nothing else was. An image named `x" & calc & ".png` closes the quote, and
everything after it runs. Severity: critical.

The fix is structural rather than a better escaping function — *escaping is a losing game played on the
attacker's board*. There is no shell now: the program and its arguments are built separately and handed
straight to the OS, so a quote inside a filename is just a quote inside a filename. Three more from the
same sweep were real too: prototype pollution through a merged sidecar patch, a world-writable temp cache
that any local account could pre-create and be trusted through, and three check-then-use races. The
regression test was proven by restoring the old shape and watching it go red.

The note that closes the entry is the honest one: *"it's a local-only backend" is mitigation, not
absolution — it is one flag away from a LAN.*

## Fairy Fox Games: Brim, and the water still in the air

The thirteenth game, and a verb the collection did not have: **pour** (`0.22.0`). A vessel arrives with a
fill line to reach and a rim not to cross. You get one pour — hold to open the spout, let go to close it.

The hook falls out of the physics rather than being bolted on. The stream is a **delay line**: what leaves
the spout lands about 130 ms later. So releasing does not stop the level rising, it stops the *source*, and
the column already in the air keeps arriving. You cannot stop where you want. You must stop **early, by
exactly the amount still falling**, and watch it land. Short of the line costs a life; over the rim costs a
life; settling in the gold band just under the rim is a *brim*, and the multiplier climbs. Greed and
survival are the same act, which is this collection's standing test for whether a mechanic is worth
planting.

It ships with varied structure from birth — a run is a seeded sequence of named pours (Steady, Slow Draw,
Stutter, Narrow Neck, Hairline, The Flood), stage-gated so climbing opens the pool. Stutter is the cruel
one: the flow alternates between a trickle and a gush, so the size of the carry changes every vessel and a
memorised release point is worse than useless.

Earlier in the day, Skyline got **the wind** (`0.21.1`) — its slabs now arrive as named, stage-gated
patterns rather than textureless drift, bringing the ninth game onto the varied-structure standard.

## Fairy Fox Stories: a grow day

Three books each gained a third chapter (`0.3.4`): *The Wintering House*, *The Cartographer of Decks*, and
*The Cinderwick Job*. No plant — the farm's three-day cadence gate said the next one is not due until the
13th, and it held rather than planting early to look busy.

## The site

The account behind all of this was renamed **`junebug12851` → `1fairyfox`** (`0.15.9`) — a change spotted in
Random AI Prompt's own history and then verified against GitHub rather than taken on trust: the old profile
now 404s, so this site's footer link, its handle, and the About page's profile link were all broken.

The rename was swept through every current-state file — the site config, the project data, the hub registry
and standards, the templates, and the **shared chrome bundle** that every project's docs site pulls, so the
nodes pick the fix up on their next refresh. Dated history — the sessions, the changelog, these posts — was
deliberately left as it was, because it records what was true on the day.

One consequence is left open rather than acted on: the hub repository is still *named*
`junebug12851.github.io`, so it is no longer a GitHub "user site" in the strict sense. Nothing is broken —
everything here is reached through the `fairyfox.io` custom domain — but the claim was false in several
documents, and correcting the *claim* is a maintenance change while renaming the repository is not.
