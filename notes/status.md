# Project Status

_Current state only._ For the chronological history see [`sessions/`](sessions/README.md);
for the commit-by-commit changelog see [`version.md`](version.md).

**Version:** `0.1.0` (single source of truth: repo-root `VERSION`; see
[`reference/versioning.md`](reference/versioning.md)).

## Current state (read this first)

**The site is live** at https://junebug12851.github.io/ (2026-06-22). It's a
clean, custom Jekyll build — no external theme — deployed to GitHub Pages by
GitHub Actions on every push to `main`; the first deploy ran green (build +
deploy) and the home/projects/blog/about pages, feed, and sitemap all serve. The
structure is in place end to end:

- **Site:** home, `/projects/`, `/blog/`, `/about/`, a first blog post, RSS feed,
  SEO tags, sitemap. Custom responsive CSS with light/dark.
- **Hub:** [`../hub/`](../hub/) holds the cross-project standards + templates and
  the project registry. This is what other repos pull.
- **Notes:** this living-notes system, mirroring the convention used across my
  projects.
- **Sync:** the pull-only cross-project model is documented
  ([`reference/cross-project-sync.md`](reference/cross-project-sync.md)) and the
  two reference repos are cloned under `assets/references/` (git-ignored).

## In flight / awaiting

- **Custom domain `fairyfox.io`.** `CNAME` is committed and the site builds it,
  but the domain is **not yet active**: DNS has no records pointing at GitHub
  Pages, and the domain isn't set in Settings → Pages yet. Add the DNS records
  (apex A/AAAA to GitHub Pages IPs, or ALIAS/ANAME → `junebug12851.github.io`),
  then set the custom domain in Settings → Pages and enable Enforce HTTPS once
  the cert issues. Until then the site lives at `junebug12851.github.io`.
- **First project round-up post.** Pending a real diff to report (see
  [`reference/blogging-workflow.md`](reference/blogging-workflow.md)).

## Next

See [`plans/next-steps.md`](plans/next-steps.md). Headline items: confirm the
first Actions deploy is green, wire DNS for the custom domain, and write the
first real "what changed in my projects" round-up once there's a diff to report.

## Health

| Area | Status |
|------|--------|
| Jekyll config + layouts | ✅ Scaffolded |
| Content pages (home/projects/blog/about) | ✅ Live |
| Pages deploy workflow | ✅ First run green; site live |
| Custom domain | ⏳ CNAME committed; DNS + Settings pending |
| Local build verification | ✅ `bundle install` + `jekyll build` green (Ruby 3.3.11) |
