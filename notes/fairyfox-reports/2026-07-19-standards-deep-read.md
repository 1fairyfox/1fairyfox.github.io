---
date: 2026-07-19
procedure: roundup
node: fairyfox.io (hub)
outcome: checked-only (findings reported; hub NOT modified pending go-ahead)
hub_version: 0.17.0
---

# Hub inbound deep-read — standardizable conventions across the siblings

Owner-directed pass: refresh the dev mirrors and **manually read every sibling `CLAUDE.md`
+ non-log notes file** (excluding session logs and changelogs) looking for conventions worth
promoting to `hub/standards/`. After this, ongoing capture reverts to the process reports.

## What was read

Mirrors refreshed on `dev` (games `5d89b0cc→a2262666`, stories `82b5a5b8→f8890f8d`, pse2
`4d2ffc8c→867408d6`, RAP up-to-date `2f1459ff`). Read all four `CLAUDE.md` in full and the
convention-bearing notes (context/principles, reference/*, working-agreements, RAP's
`2026-07-02-shareable-systems-roundup` proposal report). Domain knowledge (pse2 Gen-1
internals, RAP DPL, stories craft/*) and already-adopted hub-standard copies were categorized
out as non-standardizable.

## Candidate standards (prioritized) — proposals only

**Strong / clear gaps:**

1. **Testing & verification standard** — *no hub standard exists*, yet all four projects have
   strong, similar practice: pure-logic/rendering split for headless testability (games:
   `*.core.js` + `*.core.test.js`), **real multi-layer tests, not token ones**, a regression
   test shipped with every bug fix, run the gate before shipping, and a console/emulator oracle
   (pse2 `tst_emu_parity`). RAP explicitly proposed a `regression-testing` standard. Biggest gap.
2. **Engineering-quality standard** — "no hacks / no temp fixes / do the long work / a
   90%-done phase is not done / best craftsmanship always." Stated in pse2, games, stories.
   (Matches the standing quality bar; no hub doc codifies it.)
3. **Repo-hygiene guardrails** (RAP's headline proposal) — a doc-drift broken-link checker + an
   uncommitted-file guard wired into the test gate, plus branch-litter auto-delete with the
   non-obvious **work-branch deletion-protection** interaction. Portable scripts → `hub/templates/`.
4. **Preview-before-ship / visual review** — games + stories both mandate previewing UI/visual
   changes in Chrome (hard-reload, self-critique) before releasing; pse2 has the screenshot
   review discipline. Generalizable QA rule (could live in the testing standard).

**Worth doing:**

5. **Research-lands-in-the-notes** (pse2 standing rule) — new understanding is written to
   `notes/` in the same session, by default. A knowledge-capture discipline generalizable to all.
6. **Docs: current-vs-historical** (RAP proposal) — sweep current-state docs on every
   rename/removal; banner removed-feature docs; never edit dated history.
7. **Self-hosted fonts / no third-party hot-links** — games + stories mandate self-hosted fonts
   for privacy. **The hub itself is out of compliance** (it hot-links Google Fonts + cdnjs — now
   disclosed in its legal pages). Either a standard both adopt, or a recorded hub exception.
8. **Agent working-rhythm / collaboration** — task-tracking early+comprehensive, background work
   + foreground-when-ready-to-look, and **"adjacency is not a brief"** (don't absorb un-briefed
   neighbouring features). pse2's collaboration.md + RAP's working-agreements.md are the sources.
9. **Farm operating-model** — games + stories share the farm shape (grow daily, plant new,
   distinct-not-reskin, simple-but-deep, blueprint/plan-first, first-class-not-throwaway). A
   shared standard for the integrated **farm** tier.

## One inconsistency needing a decision

**Release-to-`main` posture differs across siblings:** games = "release by default if tests
pass"; stories = "get explicit approval first"; hub/pse2 = "release by default." Worth a single
brand decision (or an explicit per-project-configurable posture) rather than silent divergence.

## Next

Report presented to the owner; **author nothing until a go-ahead picks the set** (promoting a
standard is a deliberate act — each needs a `## Verify` slice + a `compliance.md` row + template
reflection). Ongoing capture continues via the process reports.
