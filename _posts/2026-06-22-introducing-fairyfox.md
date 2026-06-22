---
title: "Introducing fairyfox.io"
subtitle: "What this site is and why I built it."
date: 2026-06-22
tags: [meta, site]
---

This is the first post on a site that finally gives my work a single front door.

For a long time my projects have lived as separate GitHub repositories with no
central index — nothing that says what I'm building and how the pieces relate.
`fairyfox.io` fixes that. It's a small, fast [Jekyll](https://jekyllrb.com/) site
that deploys itself on every push, so keeping it current takes almost no effort.

## What it does

The site has three jobs:

1. **A hub for my projects.** The [projects page](/projects/) is generated from a
   single registry, so it stays current. It currently lists
   [Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
   and [Random AI Prompt](https://github.com/junebug12851/random-ai-prompt), with
   more to follow.
2. **A blog.** Short write-ups of what I'm building and learning, including
   periodic round-ups when something meaningful changes in one of my
   repositories.
3. **Shared standards.** The common conventions my projects use — the git
   workflow, the living-notes system, versioning, and ready-to-copy templates —
   live here, so I'm not reinventing them in every repository.

## How the repositories connect

The part I find most useful is how this hub connects to my other projects without
coupling them together. The hub holds the canonical standards; each project pulls
them in on demand through a plain shallow `git` operation — no submodules, no live
dependency, no build-time coupling. In the other direction, the hub keeps
read-only copies of the projects so I can see what changed and write about it.
Communication is one-directional `git` in each direction, which keeps every
repository independent and avoids any circular updates. The full model is
documented in the repository under `notes/reference/cross-project-sync.md`.

That's the goal: one current place to find my work, and a clean, shared structure
that makes everything easier to maintain.
