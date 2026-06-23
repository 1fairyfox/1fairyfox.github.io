---
title: "Pokered Save Editor 2: recovering a corrupted working tree"
subtitle: "A bulk rename truncated dozens of files on disk. Here's how the project was rebuilt and why the fix is a permanent rule."
date: 2026-06-06
tags: [pokered-save-editor-2, update]
---

The 2026 revival of [Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2)
— the Qt 6 / C++ rewrite of the original save editor — began with a setback worth
recording, because the recovery from it shaped a standing rule for the project.

A bulk `sed -i` rename run over the editor's working copy silently truncated 55
source files and 8 notes on disk. The tooling that performed the rename was doing
partial writes under load, and it had also been reporting some reads as truncated
when they were intact. Because the damage had already been committed, the latest
commit was not a usable restore point.

The tree was reconstructed from prior working-session transcripts, which record
every file read and write in full. Most of the ~45 affected source files came back
exactly; a handful of large files were rebuilt by replaying their recorded edit
history onto a known-good 2020 baseline, then validated line by line against the
most recent reads. The end state was verified mechanically: 380 source files, none
truncated, no missing license headers, no leftover corruption markers. After that,
the recovered tree was taken from "compiles" to "compiles, links, runs, and matches
the previous build's behaviour" by working through the residual defects one at a
time.

The lasting outcome is a hard rule, now written into the project's contributor
docs: never bulk-edit files with shell stream tools over this working mount — use
real editors or verified file writes, and check every write. Save-data fidelity is
the whole point of this editor, so the same caution that protects a player's save
file now protects the source that edits it.

Alongside the recovery, a project-wide documentation pass kicked off: the shared
`common` layer is now fully doc-commented and serves as the style reference for the
rest of the codebase.
