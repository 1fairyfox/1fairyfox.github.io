---
title: README structure & cross-linking
nav_title: README cross-linking
category: standards
order: 34
summary: A project's README travels far beyond the site — GitHub, npm, plugin registries, mirrors — where the site chrome doesn't exist, so it must carry the mesh links in its own text — a docs link near the top, a grouped "Get it" section, and a fairyfox.io footer near the bottom.
---

A project's README is the most-travelled document it owns, and out on GitHub, npm, or a
plugin registry it has none of the site chrome — no header, no navigation, no footer tying
it back to the mesh. So the README has to carry those links itself. The canonical machine
copy of this standard, with the copy-paste block, is in the repository at
`hub/standards/readme.md`.

## The rule

Three worded link placements are required, around whatever content the README already has:
a **documentation link near the top** (pointing at the project's page on the shared domain),
a grouped **"Get it" section** gathering every place the project is used, downloaded, or
published — the live app, releases, and each store or registry it ships to, labelled and
organized rather than dumped as raw URLs — and a **fairyfox.io footer near the bottom** that
links back to the hub and states the project is part of the Fairy Fox mesh.

## Why worded links, not just badges

Badges front the top of every README already, but a badge is an image: easy to skim past,
and invisible in plain-text views and some registries. A worded, labelled link survives
where a badge doesn't, and it's the thing a reader actually follows. The two are
complementary — the badge is a glanceable signal, the link is the door. The docs link and
the mesh footer apply to every project without exception; a store or deploy link is present
whenever that destination exists, and omitting one that does exist takes a recorded
exception rather than a silent drop. Complements
[README badges](/docs/badges/) and the on-site [docs-site](/docs/docs-site/) chrome.
