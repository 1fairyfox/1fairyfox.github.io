# Adopting Updates — bringing hub changes into a project

How a project that's already in the mesh **pulls and applies** later changes from
the hub: updated standards, structure, templates, specs, shared conventions — any
canonical artifact that lives in the hub and the project mirrors.

> Canonical, project-agnostic version (the one other repos copy). First-time
> bootstrap is a different procedure: [`new-project-setup.md`](new-project-setup.md).
> The model behind both: [`cross-project-sync.md`](cross-project-sync.md).

For AI or human. This flow is **outbound**: the project reads the hub. It is
**on explicit request only** — never scheduled, never auto-chained (that's what
prevents recursion across repos).

## The model in one line

**You re-read a read-only copy of the hub, diff what changed, and copy the
relevant pieces into the project by hand — then commit them locally.** Adopting a
standard is a *copy*, not a live link, so applying an update is always a
deliberate, reviewable edit.

## Steps

### 1. Refresh the read-only hub clone

```sh
git -C assets/references/fairyfox.io pull --depth 1 --ff-only origin dev
```

**If the `--ff-only` pull aborts** (the hub's `dev` was force-pushed / rewritten,
so the shallow clone can't fast-forward), don't fight it — **delete and re-clone
fresh**:

```sh
rm -rf assets/references/fairyfox.io
git -C assets/references clone --depth 1 --branch dev \
    https://github.com/junebug12851/junebug12851.github.io fairyfox.io
```

The clone is git-ignored, so re-pulling or re-cloning never produces a commit.

### 2. See what changed since you last adopted

Compare the refreshed hub copy against what the project currently mirrors, and
decide what's worth bringing over:

```sh
# example: how the project's git standard differs from the hub's now
diff -u notes/reference/git-workflow.md \
        assets/references/fairyfox.io/hub/standards/git-workflow.md
```

Skim the hub's recent changelog (`notes/version/`) to understand *why* something
changed before you adopt it.

### 3. Apply by hand, per category

Bring each kind of change into the project's own tree. Reconcile with any local
edits — the project's copy may legitimately diverge.

| What changed in the hub | Where it lands in the project | How to apply |
|-------------------------|-------------------------------|--------------|
| **Standard** (git, versioning, notes, sync, AI-context) | `notes/reference/<name>.md` | Merge the new guidance into the project's copy; keep project-specific deviations, note them. |
| **Structure** (notes skeleton, folder layout) | `notes/` tree | Add new files/sections; don't blow away existing content to match the skeleton. |
| **Spec / convention** (a shared rule or format) | wherever the project encodes it | Update the project's implementation and its doc to match the new spec. |
| **Template** (`CLAUDE.md`, `.gitignore`, `VERSION` format) | repo root | Port the meaningful change; never overwrite the project's filled-in identity. |
| **Design / shared asset** | the project's own design layer | Adopt the *intent*; the hub holds the convention, the project owns its rendering. |

Rule of thumb: **copy the change, not the file.** A blind file overwrite usually
clobbers project-specific work — diff, then hand-merge.

### 4. Record it in the project

Per the standing maintenance loop:

- Append a line to today's session log (`notes/sessions/YYYY-MM/YYYY-MM-DD.md`).
- Add the plain-English changelog entry to the top of
  `notes/version/YYYY-MM.md`, in the **same commit**.
- Bump `VERSION` if warranted (PATCH default, MINOR for a milestone, never MAJOR).
- Update `notes/status.md` if the adoption changed the project's state.

### 5. Commit, push, fast-forward `main`

On `dev`, staging specific files:

```sh
git add notes <other-touched-files>      # never -A; never assets/references/*
git commit -m "chore: adopt hub updates (<what>)"
git push origin dev

git checkout main && git merge --ff-only dev && git push origin main
git checkout dev
```

## When the project has diverged

If the project deliberately departs from a hub standard, **keep the divergence**
and write down *why* (a line in the project's copy of the standard, or its
`decisions/` notes). Adoption is not "match the hub exactly" — it's "take what
improves the project, on purpose." The hub is the source of truth for the shared
*default*, not a mandate.

## Verify

- `git status` is clean; `assets/references/` stayed untracked/ignored.
- The adopted change is present in the project's own tree (not just the
  reference clone).
- Changelog + session log + (if bumped) `VERSION` ride in the same commit.
- If the project builds/serves, it builds green.

## Anti-recursion reminders

- Pulls are **manual / on request**, never scheduled to chain.
- The flow is **read-only on the hub side** — never push into the hub as part of
  adopting from it.
- Reference clones are **git-ignored** — refreshing one never creates a commit,
  so it can't trigger anything downstream.
- A standard becomes part of the project by **copy**, not a runtime dependency
  that re-resolves.
