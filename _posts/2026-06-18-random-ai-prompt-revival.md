---
title: "Random AI Prompt: a 2026 revival — ES modules, Node 24, and full docs"
subtitle: "A dormant 2022 prompt generator is modernised to ES modules on Node 24, reorganised, and documented end to end."
date: 2026-06-18
tags: [random-ai-prompt, update]
---

Attention this week turns to the other project in the hub:
[Random AI Prompt](https://github.com/junebug12851/random-ai-prompt), a JavaScript
prompt generator for Stable Diffusion. It was largely a late-2022 / early-2023
effort — a substantial one — and then dormant until now. This day was its revival.

The codebase was modernised to ES modules targeting Node 24, the current LTS, with
every dependency taken to its current major. The bulk conversion of around 123 files
was done with throwaway codemods and then finished by hand for the entry points and
the trickier loaders, with a few genuine ES-module pitfalls captured for reuse — most
notably that imports run before top-level statements, so the old "change directory at
the top of the file" trick had to be pulled out into its own first import. An import
smoke test that loads the entire module graph, all 113 dynamic-prompt generators, and
expands a sample prompt confirmed the port is behaviour-preserving.

The tree was then reorganised so that all code lives under `src/` and all prompt
content under `data/`, with runtime and user data left at the root — a careful change,
since the loaders resolve paths relative to files rather than the working directory.
To prove the modernisation lost nothing, the original pre-revival source was pinned as
a read-only snapshot and diffed against the current tree: no files dropped, all curated
content matching line-for-line, and every code difference accounted for as either
formatting or an understood, deliberate refactor.

Finally, the project was brought up to the same management system as its sibling: the
living-notes structure, a single-source version number, a documentation site, and
CI/release workflows. The documentation went all the way to per-function coverage
across the whole codebase — the server engine, all 113 generators, the classic
frontend, and the React web app — settling on JSDoc with the notes wired in as
tutorials, producing one site of around 244 pages.
