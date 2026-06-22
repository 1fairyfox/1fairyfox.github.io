---
title: Versioning
nav_title: Versioning
category: standards
order: 2
summary: Semantic Versioning with a single source of truth in a VERSION file.
---

Projects use [Semantic Versioning 2.0.0](https://semver.org/) as the
people-facing version number. The canonical machine copy of this standard is in
the repository at `hub/standards/versioning.md`.

## The number

`MAJOR.MINOR.PATCH`

- **PATCH** is the default — fixes and ordinary changes alike. It is uncapped
  (`0.1.7`, `0.1.42`, and so on).
- **MINOR** marks a genuine milestone.
- **MAJOR** (the move to `1.0.0`) is a deliberate "stable" promise and is never
  bumped automatically.

When the choice between PATCH and MINOR is unclear, PATCH is used.

## Single source of truth

The version lives on one line in a repository-root `VERSION` file, and nowhere
else. Nothing hardcodes a version elsewhere; anything that needs to display it
derives it from that file. The number is bumped in the same commit as the change
that warrants it.

## Changelog vs. version number

The version number is the *label* (where a build is); the changelog is the
*story* (what changed, per commit). They are maintained together but are not the
same thing — see [the notes system](/docs/notes-system/).
