# Next Steps

Ordered, current. Check off / remove as done; the history lives in
[`../sessions/`](../sessions/README.md).

## Now (get it live)

- [x] Create the GitHub repo `junebug12851.github.io` (public), push `dev` + `main`.
- [x] Enable Pages via Actions; first deploy green.
- [x] Local build check (`bundle install` + `jekyll build`, Ruby 3.3.11).
- [ ] **Wire the custom domain** — at the registrar, point `fairyfox.io` at GitHub
  Pages (apex A/AAAA to `185.199.108–111.153` + IPv6, or ALIAS/ANAME →
  `junebug12851.github.io`); optionally `www` CNAME → `junebug12851.github.io`.
  Then set the domain in Settings → Pages and enable Enforce HTTPS once the cert
  issues. (The `CNAME` file is already committed.)

## Soon (make it real)

- Write the first genuine **project round-up** post once there's a diff to report
  (see [`../reference/blogging-workflow.md`](../reference/blogging-workflow.md)).
- Flesh out `/about/` with whatever I want public.
- Add an Open Graph share image (`assets/og.png`) referenced by `jekyll-seo-tag`.
- Decide whether to schedule a recurring "check projects, draft round-ups" pass.

## Later

See [`future.md`](future.md).
