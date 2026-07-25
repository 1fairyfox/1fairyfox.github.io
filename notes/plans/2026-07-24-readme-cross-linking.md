# Plan — README structure & cross-linking standard (2026-07-24)

## The ask (owner, live)

Every project's README must carry the mesh links in its own text — because the README
travels far beyond the site (GitHub, npm, Modrinth/Hangar, mirrors) where the site chrome
(header/nav/subnav/footer) doesn't exist. Specifically:

- **Docs link near the top.**
- **Deployed/app link** if it has a live app (Netlify is common), plus **store / plugin /
  publish pages** — everywhere the project is deployed or published — **organized and
  presented well**.
- **fairyfox.io links near the bottom.**

Owner scope decision (asked): **hub standard only, this pass. Never edit sibling repos** —
each project adopts on request (the normal mesh flow). Also confirmed the site chrome
already covers the *on-site docs pages*; this is specifically about the **README**.

## Decisions

- **New standard file** `hub/standards/readme.md` — "README Structure & Cross-Linking."
  Companion to, not a replacement for, [`badges.md`](../../hub/standards/badges.md) (the
  badge block) and the on-site docs-site chrome. Badges = glanceable image-signals at the
  very top; this standard = the **worded, organized links** a reader follows and that
  survive where badges don't render.
- **Required shape (top→bottom):** title/tagline → badge block (badges.md) → **docs link,
  worded, near top** → **"Get it" links section** (live app / download / store+registry /
  source, grouped + labelled) → project content → **mesh footer, near bottom** (back to
  fairyfox.io + "part of the Fairy Fox mesh").
- **Governance = complete-by-default**, same as badges/details: docs link + mesh footer
  always required; publish/deploy/store rows present whenever the destination *exists*; a
  present-destination omission is a **recorded user exception**, never a silent AI drop.
  One source of truth (link, don't restate registry/docs). Reconcile, don't clobber.
- **SemVer:** MINOR (a new standard) → `1.5.3 → 1.6.0`.

## Work breakdown (hub-side only)

1. `hub/standards/readme.md` — the standard + a `## Verify` table.
2. `hub/templates/README-links.md` — copy-paste snippet (docs line + Get-it block + mesh
   footer), and add its row to the `hub/templates/README.md` index table.
3. `_docs/readme.md` — docs-library summary page (category `standards`, next order).
4. Wire enforcement:
   - `hub/standards/compliance.md` — add the matrix row.
   - `hub/standards/onboarding-existing-project.md` + `new-project-setup.md` — add a
     README-links verify row/step (alongside the existing badges row).
   - `hub/standards/adopting-updates.md` — no structural change (it reads the changelog).
   - Regenerate `hub/standards/VERIFY-INDEX.md` via `build-verify-index.mjs`.
   - `hub/standards/CHANGELOG.md` — add the entry.
5. Notes: session log + changelog + `VERSION` bump; self round-up blog (site standard).
6. Build (`jekyll build`) + doc-link gate green; release `dev → main` via PR (MINOR path
   direct-from-dev is fine per git-workflow for a standards change with no bake needed).

## Open items

- The docs-library `_docs/badges.md` summary still says "as many applicable badges as the
  project supports" (pre-`badges.md`-strictening wording). Out of scope here; noted for a
  future docs-lifecycle sweep, not fixed in this release.
