---
layout: page
title: About this site
subtitle: What fairyfox.io is and how it's organised.
permalink: /about/
---

fairyfox.io is the project hub and documentation library for the software work of
Fairy Fox ([@junebug12851](https://github.com/junebug12851) on GitHub). It brings
together three things in one place:

- **An index of the projects** — see [Projects](/projects/), generated from a
  single registry so it stays current.
- **A documentation library** — see [Docs](/docs/): an overview of how the
  projects fit together, the shared engineering standards behind them, and an
  entry point into each project's own documentation.
- **An updates log** — see the [Blog](/blog/): notes on what's changing, including
  round-ups of changes across the projects.

## How it's built

The site is a static [Jekyll](https://jekyllrb.com/) site with no external theme,
built and deployed by GitHub Actions on every push — there is no manual publishing
step. It is hosted on GitHub Pages as a user site and served at the custom domain
`fairyfox.io`. Because the custom domain is set on the user site, each project's
own GitHub Pages site is served under the same domain (for example,
`fairyfox.io/pokered-save-editor-2/`), so the navigation links straight into a
project's documentation.

## How it stays current

Behind the site is a structured, living set of notes — the same notes system the
projects use — so the repository documents itself and anyone opening it can get
oriented without external context. The documentation in the [library](/docs/)
covers the conventions shared across the repositories.

The source for this site is public: it is the repository that hosts it.
