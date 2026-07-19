# Plan — Coins (cross-site reading-engagement points)

_2026-07-19. Target release: **0.17.0** (MINOR — new feature). Chrome bundle → **2.1.0**._

## Goal

A subtle-but-noticeable **coin** button beside the reader ("Aa") button. Reading a
page you haven't seen **today** — anywhere on the fairyfox.io origin — earns a coin.
Coins are a light **extra-reward** layer any project can tap; explicitly **not** a gate
or an access-control currency. Games can make the easiest use of it.

## Decisions (confirmed with Fairy Fox)

- **Wallet scope: per-origin, native.** One wallet shared across everything served under
  the `fairyfox.io` origin (hub + games + static docs) via a versioned origin-wide
  localStorage key — same mechanism the reader menu already uses. Netlify-hosted **apps
  are a separate origin** and keep their own wallet; sub-*domains* are out of scope (the
  user is fine excluding them — "I know it doesn't work that way"). No cross-origin bridge
  (storage partitioning makes it fragile).
- **Earn feedback: playful** — a coin pop + glow and a floating `+1`/`+2`, reduced-motion
  guarded.
- **Button click: mini panel** — balance, earned today, lifetime, one-line "how it works".
- **Driven by the navbar/chrome** so every page that wears the chrome contributes. Shipped
  as a new master JS file the bundle pulls, exactly like `reader.js`/`nav.js`.

## Earning rules

- Key a view by `location.pathname` (normalized). State is per **local day**; rolls over
  at midnight (keeps the balance, resets the day's seen-set + bonus counter).
- **First view of a page today:** +1, with a **10%** chance of +2 instead.
- **Repeat view of a page already seen today:** **1%** chance of +1, capped at **10**
  such bonuses per day (after the cap, no more repeat rolls that day).
- Award at most one grant per page load.

## Data model — `fairyfox:coins:a` (versioned, origin-wide)

```
{ coins, earned, day:"YYYY-MM-DD", seen:{ "/path/": amt }, bonus, todayEarned }
```
`coins` = spendable balance; `earned` = lifetime (never decreases); `bonus` = repeat
bonuses awarded today (cap 10); `todayEarned` = coins earned today (panel display).

## Public API — `window.FairyFoxCoins`

`get()` · `earnedTotal()` · `earnedToday()` · `onChange(cb)→unsub` · `spend(n, reason)→bool`
(false if insufficient — callers must degrade to "extra reward", never gate) ·
`reward(n, reason)` (careful, small, engagement-tied). Also dispatches a
`fairyfox:coins` DOM event `{ balance, delta, reason }` for games to listen on.

## Work breakdown (by file)

**Site**
- `assets/js/coins.js` — wallet + daily logic + button/panel injection + coin-pop + API.
- `assets/css/main.css` — `.ff-coin-*` button/panel/pop after the reader block; reduced-motion guard.
- `_layouts/default.html` — load `coins.js` (defer) after `reader.js`.
- `legal/{privacy,terms,cookies}.md` — NEW served pages at `/legal/…`, accurate to the
  code (static Jekyll on Pages, no accounts/no server storage, localStorage for reader
  prefs **and** coins, Google Fonts + cdnjs IP flag, Pages as processor, 18+ n/a). Closes a
  pre-existing legal-docs gap (the hub served none).
- `_includes/footer.html` — link the new legal pages (footer bar).
- `projects.md` — move "How the projects connect" **below** the Farms section.

**Hub / standards (chrome flows outward to siblings on re-adopt)**
- `hub/standards/docs-site/chrome/footer.html` — add the project's legal links to the
  "This project" column (convention path `/{{FF_PROJECT_KEY}}/legal/…`, adjustable).
- `hub/standards/docs-site/chrome/README.md` + `12-shared-chrome.md` — list `coins.js` in
  the pulled-files set + load steps; note the legal footer links.
- `hub/standards/docs-site/04-components.md` — brief coin-button note.
- `hub/standards/docs-site/chrome/VERSION` — 2.0.0 → **2.1.0**.
- `hub/standards/legal-docs.md` — note engagement/points local-storage counts as data to
  disclose. `hub/templates/legal/{privacy,cookies}.html` — add the engagement/coins line so
  new + re-adopting projects disclose it.

**Notes**
- Session log `notes/sessions/2026-07/2026-07-19.md`; changelog atop
  `notes/version/2026-07.md`; bump root `VERSION` → 0.17.0; refresh `notes/status.md`.

## Verify

Local `jekyll build` green; coin button renders beside "Aa" in light/dark; earning a coin
pops + persists across pages and reloads; day rollover resets the seen-set not the balance;
`window.FairyFoxCoins.get()` reflects the balance; legal pages render and are linked. Hold
the `main` release for an explicit go-ahead (Fairy Fox is mid-iteration).

## Not doing (scope guards)

- No cross-origin/app bridge. No gating/exclusive-access spend. No server. Not touching the
  font strategy (disclosing the current Google Fonts/cdnjs use truthfully, not changing it).
- Siblings adopt the new chrome (coins + footer legal) on-request, not auto-chained.
