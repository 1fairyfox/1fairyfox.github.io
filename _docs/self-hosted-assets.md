---
title: Self-hosted assets
nav_title: Self-hosted assets
category: standards
order: 27
summary: A published mesh site makes no third-party requests for its own presentation — fonts and controlled assets are served from its own origin.
---

A published mesh site makes **no third-party requests** for its own presentation. Fonts, icon
fonts, and any static asset it controls are self-hosted from its own origin — never hot-linked
from Google Fonts, a public CDN, or similar, which leak the visitor's IP to that third party on
every page load. Distilled from the games and stories farms, which both mandate self-hosted
fonts. The canonical copy is in the repository at `hub/standards/self-hosted-assets.md`.

## The rules

- **Self-host the fonts.** Ship the font files from the site's own origin and reference them
  locally. Don't hot-link Google Fonts, Typekit, or a public font CDN.
- **No third-party hot-links for controlled assets.** Icon fonts and CSS/JS the site owns are
  vendored and served from the site — not pulled from a CDN at read time. (Genuinely external,
  user-invoked services are a different thing.)
- **The published site makes no presentation request to a third party.** On load, a visitor's
  browser fetches the site's assets from the site — nothing about them is sent to a font or CDN
  host for the page to render.
- **Keep the legal pages honest with reality.** If an asset genuinely must come from a third
  party, disclose the IP exposure and record it as an exception with a remediation path.

## Known exception (to remediate)

The hub (fairyfox.io) itself currently hot-links Google Fonts and cdnjs (Font Awesome) — a
recorded exception with a remediation path, not a licence to add more. It directly supports
[legal-docs](/docs/legal-docs/): a truthful "nothing leaves to a font or CDN provider" is both
more private and easier to state than disclosing an IP leak.
