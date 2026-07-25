---
title: "A README that carries its own map"
subtitle: "A new shared standard: because a project's README travels to GitHub, npm, plugin registries, and mirrors — everywhere the site's header, nav, and footer don't reach — it has to carry the mesh links in its own text. A documentation link near the top, an organized section for wherever the project is published and deployed, and a link back to fairyfox.io near the bottom."
date: 2026-07-24
tags: [site, update]
---

Every project's documentation pages wear the shared site chrome — the same header, navigation, and
footer — so from inside `fairyfox.io` you always have a way to the docs, to the other projects, and
back home. A README doesn't get any of that. It travels: it renders on GitHub, on npm, on a plugin
registry like Modrinth or Hangar, inside a package manager, on a fork or a mirror. In all those
places it is on its own, with no chrome to lean on. If it doesn't carry the links itself, a reader
lands there and has no thread back to anything.

So the hub gained a standard that says a README carries three things in its own text. A worded
documentation link near the top, pointing at the project's page on the shared domain — not just the
docs badge, which is an image easy to skim past and invisible in plain-text views. A single organized
section gathering wherever the project actually lives: the live app if it's deployed, the release and
download links, and a labelled row for every store or registry it publishes to — presented as a
scannable list, never a wall of raw URLs. And a short footer near the bottom that links back to
fairyfox.io and says, plainly, that this is one project in a larger mesh.

The rule is complete by default, the same posture the badge set already uses: the documentation link
and the mesh footer are required for every project, and a publish or deploy link is present whenever
that destination genuinely exists — a missing one is only acceptable because there's nothing to link
yet, and it goes in the moment there is. The standard ships with a copy-paste block, a Verify check,
and a place in the compliance audit and both onboarding runbooks. Nothing in the sibling repositories
changed today; each adopts the standard on its own, the way the mesh always works.
