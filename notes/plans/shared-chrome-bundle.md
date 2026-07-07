# Plan — Shared chrome bundle + Stories nav (0.15.0)

Two requests, one release:

1. **Add `fairyfox-stories` to the primary nav**, immediately left of Games.
2. **Make the shared chrome genuinely reusable** — one canonical bar, subnav,
   footer, reader/theme, and palette that projects adopt as *exact copies* instead
   of hand-reimplementing (which is why every project's header/reader/footer has
   drifted). Deliver clear, adoptable standards.

## The decision (from Fairy Fox)

- **Sharing model:** the shared chrome assets are **hosted here (the hub) and pulled
  over git at build time** into each project. Vendored **exact copies**, not a
  runtime hot-link — so the mesh stays decoupled (a built project is self-contained
  and offline-safe; a bad hub change can't live-restyle every deployed site), but the
  copies are byte-identical instead of reimplemented from a spec. This is a
  **deliberate revision** of the old "reimplement, don't copy a CSS file" line of the
  docs-site standard — narrowed: the *chrome* is now a vendored bundle; the tokens/
  layout/page-content spec still governs everything the generator styles itself.
- **Stories nav:** behaves exactly like Games — a nav item that takes you to the
  project's page. `Stories` → `/stories/` stub → `/fairyfox-stories/` (mirrors
  `/games/` → `/fairyfox-games/`).
- **Scope:** hub-side only + the new standards. **No sibling edits** — projects adopt
  on request (pull-only mesh). Registering `fairyfox-stories` as a tracked project
  (cards, `projects.yml`/`registry.yml`, integrated tier) is a **deliberate
  follow-up** — it needs the project's real metadata, and the registry honesty rule
  forbids seeding fabricated version/lifecycle. This release wires the nav only.

## Why a bundle (not just a better spec)

Reimplementing header/reader/footer per stack guarantees drift: RAP, pse2, and the
generated Doxygen output each grew a slightly different bar/reader/footer. The design
*tokens* are legitimately spec-and-reimplement (they touch every page a generator
emits). The **chrome** is a fixed, framework-agnostic shell — the same HTML + the same
two vanilla JS files + the same stylesheet on every site. That is exactly the kind of
thing you *copy*, not paraphrase. Copying it kills the drift.

## The bundle — `hub/standards/docs-site/chrome/`

A pullable, versioned bundle. **CSS + JS are pulled from the live master paths**
(`assets/css/main.css`, `assets/js/reader.js`, `assets/js/nav.js`) so there's one
source of truth and no snapshot lag; the bundle ships the **static HTML** the Liquid
`_includes/` can't be used as directly, plus the adoption contract.

```
chrome/
  README.md            # what it is · the git-pull contract · placeholder tokens · versioning · sync-from-master
  VERSION              # bundle semver (1.0.0)
  head.html            # <head> chrome: pre-paint theme script + fonts + theme-color metas
  header.html          # header + primary nav (Stories added) + reader-button note
  subnav.html          # secondary-nav template ({{FF_SUBNAV_ITEMS}})
  footer.html          # footer template ({{FF_PROJECT_KEY}} / {{FF_PROJECT_NAME}})
  adapters/
    jekyll.md          # includes + relative_url
    doxygen.md         # HTML header/footer + custom stylesheet injection
    static-and-spa.md  # hand-rolled HTML / React-Vite / MkDocs etc.
```

Placeholder contract: the primary nav, reader button, palette are **fixed** (never
edited by a project); only the marked `{{FF_*}}` slots (subnav items, footer "This
project" links, project key/name) are filled per project.

## Work breakdown

- **Site:** `_includes/header.html` (+Stories); new `stories.html` redirect stub.
- **Bundle:** the eight files above.
- **New standard:** `docs-site/12-shared-chrome.md` (the vendored-bundle spec + a
  `## Verify`). Wire it into `docs-site/README.md` (file table + soften the
  "reimplement, don't copy" framing), and reference it from `01`, `04`, `05`, `09`.
- **Compliance:** add a chrome-bundle line to `08-compliance-checklist.md`; note the
  bundle in the mesh `hub/standards/compliance.md` docs-site row.
- **Mesh-nav enumerations:** add Stories before Games everywhere the fixed set is
  written out — `01`, `04`, `05`, `08`, `reference/chrome.html`, `reference/README.md`.
- **Notes/version:** changelog atop `notes/version/2026-07.md`, bump `VERSION`
  0.14.5 → **0.15.0** (MINOR — new standard + bundle + nav slot), session log.

## Release shape

MINOR. Do the work on `dev`, `jekyll build` green, commit on `dev` with the changelog
inside. **Hold the `main` release for an explicit go-ahead** — it deploys a `Stories`
nav item that points at a `/fairyfox-stories/` page which may not be live yet, so
confirm before shipping to production. Report, then wait.
