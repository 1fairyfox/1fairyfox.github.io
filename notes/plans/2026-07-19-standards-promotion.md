# Plan — promoting nine cross-brand standards (0.18.0)

_2026-07-19. From the [inbound deep-read](../fairyfox-reports/2026-07-19-standards-deep-read.md).
Owner directed: author all nine, phased. Target release: **0.18.0** (MINOR — a batch of new
hub standards), shipped **after** 0.17.0 (coins) is out._

## Release-posture decision (baked in)

The brand rule, resolved to **Random AI Prompt's gate** (the standards-bearer): a release to
`main` goes through a **PR** (main stays branch-protected), and you **generally wait for CI to go
green on the PR before merging** (`gh pr create --base main --head dev` → `gh pr checks --watch` →
`gh pr merge`), then hand-tag `vX.Y.Z`. This is distinct from routine `dev` pushes, which still
**don't** block on CI. Encode in `git-workflow.md` and reconcile the siblings' divergent wording
(games "release by default", stories "approval first") to: *release when the suite is green **and**
CI on the main PR passes.* Update the memory nuance: "never block on CI" applies to `dev` pushes,
**not** to the `main` release gate.

## Phasing (each standard: spec + `## Verify` + a `compliance.md` row + hub README entry)

**Phase 1 — verification & quality (the biggest gaps)**
- `hub/standards/testing.md` — pure-logic/rendering split for headless testability; **real
  multi-layer tests, not token**; a regression test ships with every bug fix; run the gate before
  shipping; a console/emulator/browser oracle where one exists; **preview visual changes before
  shipping** (folded in). Sources: games, pse2, RAP (proposed regression-testing).
- `hub/standards/engineering-quality.md` — no hacks / no temp fixes / do the long work / a
  90%-done phase isn't done / best craftsmanship; full docs + doc-comments; fearless refactoring
  behind the test gate. Sources: pse2, games, stories.

**Phase 2 — hygiene & docs**
- `hub/standards/repo-hygiene.md` (+ `hub/templates/check-links.mjs`, `check-tidy.mjs`) — doc
  broken-link gate + uncommitted-file guard wired into the test gate; branch-litter auto-delete
  with the work-branch deletion-protection interaction. Source: RAP roundup.
- `hub/standards/docs-lifecycle.md` — current-state vs dated-history: sweep current-state on every
  rename/removal; banner removed-feature docs; never edit dated history. Source: RAP roundup.

**Phase 3 — knowledge & collaboration**
- `hub/standards/research-capture.md` — new understanding lands in `notes/` in the same session,
  by default (primary-source first; probe when load-bearing; write the reference note; say what it
  means for the code; wire it up). Source: pse2 standing rule.
- `hub/standards/working-rhythm.md` — agent collaboration: task-tracking early+comprehensive;
  background work, foreground the moment it's worth a look; **"adjacency is not a brief"** (don't
  absorb un-briefed neighbours); ask-before-building when unsure. Sources: pse2 collaboration, RAP
  working-agreements.

**Phase 4 — assets & farm**
- `hub/standards/self-hosted-assets.md` — self-host fonts + no third-party hot-links (privacy: no
  visitor-IP leak). **Record the hub's current exception** (it hot-links Google Fonts + cdnjs) with
  a path to remediation. Sources: games, stories.
- `hub/standards/farm-operating-model.md` — the integrated **farm** tier: grow daily / plant new /
  distinct-not-reskin / simple-but-deep / plan-(blueprint)-first / first-class-not-throwaway.
  Sources: games, stories.

**Wire-up (Phase 5)** — add all nine to `compliance.md` + `hub/README.md`; session log + changelog
atop `notes/version/2026-07.md`; bump `VERSION` → `0.18.0`; refresh `status.md`.

## Guardrails

- **Establishment discipline:** each standard consistent everywhere it's referenced (templates,
  runbooks, CLAUDE template as relevant) + a real `## Verify` the compliance audit aggregates.
- Author from the siblings' real practice (cite the source), not invented policy. Neutral voice.
- Nodes adopt on-request; nothing here edits a node. This is hub-side authoring only.
- **Not doing MAJOR;** not auto-releasing — hold `main` for a go-ahead. 0.17.0 ships first.
