---
title: AI context (CLAUDE.md)
nav_title: AI context
category: standards
order: 5
summary: A root entry-point file that orients an AI assistant opening a repository.
---

Each repository carries a root `CLAUDE.md` file: a short entry point for an AI
assistant — or any newcomer — opening the repository without prior context. The
canonical machine copy of this standard is in the repository at
`hub/standards/ai-context.md`, with a template at `hub/templates/CLAUDE.md`.

## What it contains

1. A one-line identity for the project.
2. A "start here" pointer to `notes/status.md` and the rest of the notes.
3. The short list of project-specific things not to get wrong.
4. How to build, test, and run — stated plainly, including which tools are
   actually available.
5. The standing workflow that should happen by default (build, test, commit on
   `dev`, fast-forward `main`, with the changelog and version bump riding inside
   the commit).
6. A reminder of how the notes are kept current.

## Principles

It is an index, not a manual: depth lives in `notes/`, and `CLAUDE.md` routes to
it rather than duplicating it. Capabilities are stated honestly so an assistant
neither refuses work it can do nor attempts work it cannot. Anything meant to
happen "by default, without being asked" is written down explicitly.
