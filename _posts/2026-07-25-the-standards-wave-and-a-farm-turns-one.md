---
title: "The standards wave lands, and a farm turns one"
subtitle: "In a single day the whole mesh pulled the same span of shared standards forward together — every project adopting the 0.20.2→1.6.1 batch, hardening its supply chain, and filling out its README. The story farm used the moment to cut its first stable release, the games collection cleared the last gap in its depth layer, and the save editor spent the day on the plumbing behind its next feature."
date: 2026-07-25
tags: [fairyfox-games, fairyfox-stories, pokered-save-editor-2, random-ai-prompt, papermc-despawned-items, standards, update]
---

Most days one or two projects move. This one moved all of them at once, and around a single
theme: adoption. The hub had gathered a long span of shared standards — everything from the
0.20.2 line through 1.6.1, including the "done means verified" contracts, a per-standard
adoption manifest, complete-by-default and phased work, a local-first Docker rule, a CI-secrets
provisioning tool, and the README cross-linking standard — and on this day every node in the
mesh pulled that span forward together. Each did it the same disciplined way: refresh the
git-ignored mirror, adopt under the standing standards grant with the full safety floor kept,
and record what is *actually* adopted (with evidence) versus what is still a dated gap. What
follows is one day seen from six repositories.

## Fairy Fox Stories: a first stable release

The story farm marked **1.0.0** — its first stable release, and a MAJOR bump, which across the
mesh is only ever the owner's call. Nothing about the farm suddenly changed; it has been live and
growing since its five-book start. What 1.0.0 recognises is that the farm is now both mature and
hardened. The same day, it adopted the full 0.20.2→1.6.1 standards span, restored branch
protection on `main` (lost in the earlier account rename) with the complete CI suite required
before anything merges, wired an OpenSSF Scorecard workflow, and filled its README badge block to
sixteen of the canonical twenty — the four remaining slots being SaaS-backed ones that need
accounts only the owner can create. It cut the release the deliberate way: a `release/1.0.0`
branch, a CI-gated pull request into the protected `main`, then a back-merge. Underneath the
milestone the farm also just kept farming — **The Hundredth Wind** advanced to its third chapter,
"The First Try," the beat where a first attempt at mastery is supposed to fail.

## Fairy Fox Games: the last gap in the depth layer, then the standards

The collection closed a long-running piece of its own roadmap. Its growth lever lately has been
adding *depth inside the mechanic* — hidden scoring bands, doubling windows, and secret stages —
to games that shipped without it, and **Sluice** was the last game still explicitly named as
missing that layer. With Sluice retrofitted, the newer games all ship depth from birth and the
catch-up list is finally empty. The rest of the day was the standards span, adopted in full: every
game's README grew to the complete twenty-badge block with a worded docs link, a "Get it" section,
and a mesh footer; the five new standards were vendored; and a new adoption manifest now records
the honest per-standard state. The collection also wired its quality services — Codecov coverage
(measured at 99.84% of lines across the game cores), a dormant SonarCloud workflow that only wakes
once it's switched on, and a token-backed Scorecard workflow with the shared provisioning tool
vendored in — all of it non-blocking, so a release can never be held up by a badge.

## Pokered Save Editor 2: a day of plumbing

The save editor spent the day almost entirely below the waterline, and its version number stayed
put at 0.43.6-alpha to say so. It adopted the standards span and hardened its supply chain to the
current bar: every GitHub Action pinned to a commit, a CodeQL static-analysis workflow, build
provenance attached to releases, a Scorecard workflow, and a coverage gate. It added self-hosted
Privacy, Terms, and Cookies pages written to what the app actually does — a desktop editor that
stores nothing on a server — and wired its three authenticated CI services so the coverage, quality,
and security badges have real workflows behind them rather than tokenless shortcuts. It also *landed*
the in-progress map-screen work that had been sitting uncommitted (the reason its `dev` branch had
been red), and fixed a copy-paste bug in the test registration that had quietly kept one map test
from ever building in CI. All of it restored the pipeline to green — but none of it was a finished
feature, so the version deliberately did not move. The MINOR bump waits for the map screen to
actually ship.

## Random AI Prompt: standards, then dependencies

The prompt generator adopted the same 0.20.2→1.6.1 span — seeding its first adoption manifest, taking
in the four new standard notes, and bringing its README to the cross-linking standard with a worded
docs link, a "Get it" section, and a mesh footer (its badge block already carried all twenty in
order). That work was notes and README only, so it moved no version. It then cleared its dependency
backlog in the same release: four pending Dependabot groups, folded together superset-wins after the
bot regenerated two of them mid-flight, taking eslint, prettier, playwright and the rest to their
current versions and bumping the pinned action commits across all nine workflow files. That last part
was an ordinary change behind the project's own test gate, so it shipped as **2.60.2**.

## Despawned Items: a README that carries its own map

The Minecraft plugin had caught up to the standards the day before; today it took the one piece that
had landed since — the README structure and cross-linking standard — and applied it. A README travels
to GitHub, to plugin registries, and to mirrors where the site chrome never renders, so it has to
carry its own way home: a worded documentation link near the top, an organized "Get it" section, and
a footer tying the repository back into the mesh. That, plus a status refresh, shipped as a
documentation-only **1.5.1**, with the download-page rows for the plugin marketplaces noted as
pending until those pages exist.

## The shape of the day

Six repositories, one discipline. The visible outputs were small and honest — a chapter, a retrofit,
a hardened pipeline, a dependency sweep, a better README — but the day's real work was the mesh
proving it can move a large span of shared standards through every node at once without any of them
cutting a corner, and recording, project by project, exactly what is adopted and what is still owed.
That the story farm chose the same day to declare its first stable release fits the theme: 1.0.0 is
itself a statement that the thing behind it is verified, not just shipped.
