---
title: Maintenance sweep
nav_title: Maintenance sweep
category: standards
order: 29
summary: A documented, repeatable whole-repo tidy that returns a project to a clean shipped baseline — audit-first, act only on go-ahead.
---

A documented, repeatable **whole-repo tidy** that returns a project to a clean shipped baseline —
no stray branches, no PR limbo, current-state docs matching the code, `dev` and `main` in sync
and green. Every project runs the same sweep instead of improvising one, so drift is caught on a
cadence rather than whenever someone notices. Proposed by Random AI Prompt after a sweep found
`status.md` five versions stale, eight merged branches lingering, and an open Dependabot PR. The
canonical copy is in the repository at `hub/standards/maintenance-sweep.md`; it **composes**
existing standards rather than restating them, and like every cross-cutting procedure it is
**audit-first, act only on go-ahead.**

## The sweep

- **Audit read-only first.** Fetch and prune, then enumerate local and remote branches, open
  PRs and issues, and CI health — a complete picture before touching anything.
- **Triage PRs and issues — surface, don't auto-act.** Every open item (Dependabot PRs included)
  is a decision for the owner. An unattended run reports and waits; it never merges, closes, or
  pushes a PR on its own.
- **Close merged branches only** (`git branch -d`, never `-D`), confirmed merged first. Target
  end state: only `main` and `dev`, plus any deliberately-kept release branch.
- **Ship `dev` → `main`** per the [git workflow](/docs/git-workflow/) — including the SemVer gate
  and the mandatory back-merge so `dev` contains `main` afterward.
- **Reconcile current-state docs with the code** per [docs-lifecycle](/docs/docs-lifecycle/):
  `status.md`, the health tables, any "pending review" phrasing for work that shipped.
- **Verify and record** — run the test gate, then note the sweep in the session log.
