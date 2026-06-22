---
title: Git workflow
nav_title: Git workflow
category: standards
order: 1
summary: Branch model, fast-forward merges, and the safety rules shared across repositories.
---

The shared git standard favours a clean, faithful, low-risk history. Its
canonical machine copy lives in the repository at `hub/standards/git-workflow.md`;
this page is the readable summary.

## Branches

- **`main`** is stable and deployable, and is never committed to directly. It only
  moves by fast-forward to a known-good `dev` commit. On the hub, every push to
  `main` triggers a deployment.
- **`dev`** is the working branch, committed to early and often. It is also the
  branch the hub and other repositories track when they sync.

Feature branches are not used by default; one is added only to isolate a large or
risky change, then merged back and deleted.

## Fast-forward merges only

Because `main` is never committed to directly, `dev` is always ahead of it, so
`dev → main` is always a fast-forward:

```sh
git checkout main && git merge --ff-only dev && git push origin main && git checkout dev
```

This produces a linear history while preserving every original commit. History is
never squashed, rebased, or rewritten once pushed.

## Commits

Each commit is one focused change with a `type: summary` message (`feat`, `fix`,
`docs`, `content`, `build`, `chore`, and so on). Where a change warrants it, its
changelog entry and any version bump are made in the **same commit** rather than
in a follow-up.

## Safety rules

Force-pushing, history rewriting, hard resets, rebases, and branch deletion are
not performed without an explicit request. Files are staged individually rather
than with `git add -A`, so build output and reference clones stay out of history.
