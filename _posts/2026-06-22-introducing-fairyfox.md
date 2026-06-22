---
title: "Introducing fairyfox.io"
subtitle: "The launch of the project hub and documentation library, and how it's organised."
date: 2026-06-22
tags: [meta, site]
---

This post marks the launch of fairyfox.io and records how the site is put
together.

fairyfox.io is the hub for Fairy Fox's software projects. Until now those projects
lived as separate repositories with no shared front door; this site provides one,
along with a place to document the conventions they have in common.

## What the site provides

- **A project index.** The [projects page](/projects/) is generated from a single
  registry, so it stays current. It currently covers
  [Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
  and [Random AI Prompt](https://github.com/junebug12851/random-ai-prompt).
- **A documentation library.** The [docs](/docs/) section collects an ecosystem
  overview, the shared engineering standards, and an entry point into each
  project's own documentation site.
- **An updates log.** This blog, where changes — including round-ups of activity
  across the projects — are written up.

## How the repositories connect

The site is also a hub in a more literal sense: it holds the canonical shared
standards (git workflow, versioning, the notes system, cross-project sync), and
each project pulls them in on demand through a plain shallow `git` operation — no
submodules, no live dependency. In the other direction, the hub keeps read-only
copies of the projects so their changes can be tracked and documented. Each flow
is one-directional git, which keeps the repositories independent and avoids
circular updates. The model is documented under
[cross-project sync](/docs/cross-project-sync/).

A useful side effect of the setup: because the custom domain is configured on the
user site, each project's GitHub Pages site is served under the same domain, so
the navigation can lead directly into a project's documentation.
