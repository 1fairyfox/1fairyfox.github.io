---
title: Coins
nav_title: Coins
category: standards
order: 20
summary: A light, shared reading-engagement layer across the mesh — subtle, never a gate, never the point.
---

**Coins** are a small shared engagement layer across the Fairy Fox mesh: opening a page
you haven't read **today** — anywhere same-origin under `fairyfox.io` — earns a coin. The
counter lives in the shared chrome, beside the reader "Aa" button, and the balance is shared
across every same-origin site in the browser via one origin-wide key. The canonical machine
copy of this standard is in the repository at `hub/standards/coins.md`; the behaviour ships as
the master `assets/js/coins.js` in the shared-chrome bundle, so a project gets coins by
adopting the chrome.

## The prime directive: subtle, never central

Coins are a garnish, not the meal. They **must never be overused**. A project may add its own
coin moments, but only where they genuinely fit, and always as a *small extra* feeling.

- **Never gate.** Coins must not unlock, restrict, or grant exclusive access to anything. The
  core experience is always fully available to someone with zero coins.
- **Extra reward, not the reward.** Use coins to add a touch of delight on top of something
  already satisfying — never as the thing a user is working toward.
- **Restraint by default.** If you're unsure whether a spot warrants a coin, it doesn't.
  Sprinkle, don't shower — a project that grants coins constantly cheapens them mesh-wide.
- **Never at the brand's expense.** A coin flourish must not clutter the UI or distract from
  the project's own content. If a coin moment makes the page worse, remove it.

## Earning model (fixed — do not reimplement)

The earning rules and the `window.FairyFoxCoins` API ship in the shared bundle; a project uses
them, it doesn't re-implement them. The transparency page at `/legal/coins/` explains the model
in plain language, and the [legal-docs](/docs/legal-docs/) brand minimum requires each node to
disclose coins the same way.
