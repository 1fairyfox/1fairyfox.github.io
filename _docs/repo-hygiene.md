---
title: Repo hygiene
nav_title: Repo hygiene
category: standards
order: 23
summary: Small mechanical guardrails so drift, stranded files, and branch litter fail loudly instead of accumulating.
---

Small **mechanical guardrails** so drift, stranded files, and branch litter fail loudly instead
of accumulating — distilled from Random AI Prompt's large-restructure experience, where each of
these bit repeatedly until a guard made it self-catching. The canonical copy is in the repository
at `hub/standards/repo-hygiene.md`, with portable zero-dependency starter scripts under
`hub/templates/`.

## The rules

- **Doc-drift gate — a broken-link checker.** A script walks every tracked `.md` and fails the
  build on any relative link whose target doesn't exist. Wired into the test gate and CI, so a
  rename that leaves a dangling link turns red before it merges.
- **Uncommitted-file guard.** A script fails on any untracked, non-ignored file — the exact
  signature of "someone wrote a doc and never committed it". Run before finishing a session.
- **Nothing useful is ever left uncommitted.** Notes are committed as you go; the changelog entry
  rides in the same commit as its change; every process report gets committed.
- **Rename / move / remove → sweep the docs in the same change.** The link gate catches dangling
  links; `git grep` the old name catches prose. Fix current-state docs; leave dated history intact.
- **Delete spent branches — with one non-obvious guard.** Enable `delete_branch_on_merge`, but
  protect the long-lived work branch so the first `dev → main` release PR doesn't auto-delete `dev`.

The policy half of doc drift lives in [docs-lifecycle](/docs/docs-lifecycle/); this standard is
the mechanical enforcement.
