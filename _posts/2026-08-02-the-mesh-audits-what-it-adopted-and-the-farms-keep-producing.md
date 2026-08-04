---
title: "The mesh audits what it adopted, and the farms keep producing"
subtitle: "The day after the standards wave, every node turned its adoption manifest into a verified result — running a full compliance audit against its own tree and fixing the supply-chain gaps the check surfaced. Underneath the audits the farms kept farming: a new book, a new game, a first cross-run unlock, and a security fix that took a real scanner's word over a badge's."
date: 2026-08-02
tags: [fairyfox-stories, fairyfox-games, random-ai-prompt, papermc-despawned-items, pokered-save-editor-2, compliance, update]
---

A standards span is only worth what a node can actually prove it implemented. The day the whole
mesh pulled the 0.20.2→1.6.1 batch forward, each project recorded an adoption manifest — a
per-standard claim of what it had taken in. This day was the follow-through: node after node ran a
full compliance audit, walking every adopted standard's own `## Verify` check against its real
tree, and treating any gap between the manifest and the evidence as a bug to fix rather than a
number to round up. The recurring finding was the same everywhere — the supply-chain claims had
been marked implemented a shade too generously — and the recurring response was the same too: fix
it, verify it with the real tool, and record the honest result. Around that discipline, the farms
and the prompt generator kept shipping actual work.

## Random AI Prompt: a security fix that trusted the scanner, not the badge

The prompt generator's audit produced a hard number: its OpenSSF Scorecard sat at 6.7 against the
7.0 floor the ship contract requires — and, importantly, that figure came from the live scoring
API, not the cached badge. The dominant lever was the Vulnerabilities check reading zero, driven by
a set of known advisories mostly buried in the Rust and GTK crates behind the Tauri desktop shell.
The fix, shipped as **2.60.3**, cleared the check the honest way. Everything fixable was fixed —
`npm audit fix` at the root and the web target, and pinned transitive dependencies (postcss,
brace-expansion) in the mobile target. Everything genuinely unfixable was *documented* rather than
hidden: an `osv-scanner.toml` beside each affected manifest, cataloguing the seventeen no-fix
Tauri-Linux Rust advisories (confirmed no-fix by `cargo audit`) and a single build-time Expo
advisory — the exact mechanism Scorecard's Vulnerabilities check honours. The proof was the real
scanner: osv-scanner v2.4.0 reporting "No issues found," which moves the check from zero to full and
lifts the score toward 7.4 once the weekly rescan catches up.

## Despawned Items: the compliance sweep closes the gaps

The Minecraft plugin ran the same audit and came out compliant, with a live Scorecard of 7.9, then
closed the handful of gaps the walk surfaced — shipping as **1.5.2**. Its Dockerfile base image was
SHA-pinned to a verified digest (lifting Scorecard's Pinned-Dependencies check to full), a
nine-PR Dependabot backlog was triaged the way the ship contract asks — the green bumps merged, and
the ones that contradicted a deliberate decision (Paper's API past the 1.21.x target, a Kotlin bump
that breaks the CodeQL pin, a ktlint major that fails the build) closed with recorded reasons and
future recurrences suppressed. Two Paper server-smoke jobs were added to `main`'s required checks so
the full-CI gate is now platform-enforced across all seven jobs. The sweep also formally corrected
the dates on the prior adoption day's artifacts, which had been stamped with the hub's commit date
instead of the day the work actually happened.

## Fairy Fox Stories: a new book, and two chapters, and a hardened pipeline

The story farm had its busiest day in a while. It planted its eleventh book, **The Overcount** — a
generation-ship SF thriller set in the Long Quiet, a standalone tale in the realm of *The
Cartographer of Decks* that reads fully on its own. It is told by a new author-persona, Aster Coyle,
in a procedural voice, and in **present tense** — a first for a shelf whose narrators all speak in
past, chosen deliberately for a ticking hunt with no *later* to look back from. Its teller works the
office that keeps a sealed generation ship balanced body-for-body, one licensed birth against one
freed death, and finds the ship breathing for one body more than any register can name. The same day
the farm's daily growth run advanced two other books a chapter each — *The One-O'Clock Bus* reached
its third and *The Wind She Would Not Keep* its second, both landing the "complicity" beat their
blueprints reserved for that point. The day closed with the farm's own compliance sweep: every
workflow SHA-pinned and bumped to current majors, build provenance attached as a real release asset,
and a new `check-standards.mjs` script that machine-checks the grep-able invariants (the active nav,
and that `VERSION` matches the newest tag) as part of the test gate.

## Fairy Fox Games: an eighteenth game, and the first cross-run unlock

The collection added **Reel**, its eighteenth game and a genuinely new verb: give-and-take, resist
versus yield. A catch on the line fights back, alternating between calm stretches you can reel freely
and surges where reeling spikes the line's tension — read the reacting opponent, pour on the reel
while it's calm, ease off the instant it thrashes, and land it before three snaps end the run. Its
hidden depth is the *haul*: the exact tick a surge breaks opens a razor window where snapping back
onto the reel converts the catch's spent lunge into a burst and a growing multiplier, so the precise
line and the greedy line are the same single input. The day also made the varied-structure
standard's third rule real for the first time — the meta layer *driving* variation — by giving the
older game **Tether** the collection's first cross-run unlock: a new anchor-line, Windfall, that
stays out of the pool until the player has banked 150 lifetime whips across all their runs, gating on
the game's skill act rather than mere survival. A pair of follow-up fixes rounded out the day — Reel
got its own bespoke icon, and a CI false alarm was quieted where the release flow's two-push
back-merge was tripping the branch-sync guard on every release.

## Pokered Save Editor 2: the groundwork under the badges

The save editor spent the day on plumbing again, finishing the wiring its badges had been standing
in front of. It vendored an interactive tool to provision the three authenticated CI service secrets
locally, completed its README badge set (coverage, quality, quality-gate, tech-debt, scorecard) now
that those services resolve, and recorded the CI services and tools in its credits. One small but
real fix belonged to the account rename: SonarCloud keeps its organization key when a GitHub account
is renamed, so the project's Sonar org and project keys stay `junebug12851_*` even though the repo
now lives under `1fairyfox`. None of it moved the version — the day's feature work would land the
next morning.

## The shape of the day

The adoption day proved the mesh can move a large span of standards through every node at once. This
day proved the harder, quieter thing: that each node will then turn around and *check* what it
claimed, against its own tree, with the real tools — and treat the difference as work to do rather
than a number to smooth over. That the farms shipped a book, a game, and a first-of-its-kind unlock
in the same twenty-four hours is the point, not a distraction from it: the audits are what let the
production stay honest.
