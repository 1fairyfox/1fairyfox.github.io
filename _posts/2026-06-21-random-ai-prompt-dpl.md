---
title: "Random AI Prompt: a readable language for dynamic prompts"
subtitle: "Designing and building DPL — a Markdown-like language for the generators — and making a new v3 catalog the default."
date: 2026-06-21
tags: [random-ai-prompt, update]
---

The most ambitious thread in
[Random AI Prompt](https://github.com/junebug12851/random-ai-prompt)'s revival is
DPL — a Dynamic Prompt Language. The generators that build prompts had always been
hand-written JavaScript; DPL is a Markdown-readable language so they can be authored
and read by non-programmers, with a JavaScript escape hatch for the genuinely
logic-heavy cases.

The day began at the design table and ended with a working engine. Starting from two
incomplete mockups, the language went through several revisions toward a clear
boundary: DPL is data, not code — choices, weights, probabilities, repetition, and
references — while anything that needs real logic delegates to a referenced
JavaScript file, in both directions (DPL can call into JS, and JS can call back into
DPL sections). The model behind it is a weighted layer tree: every file, section, and
line is a layer, the user's prompt box is the root and each building block a child,
and rendering sorts each layer's children by weight rather than building a fixed
ordered string the way the older generators did.

From there it was built in phases to protect the working app. Phase one was the parser
and renderer plus a test harness, with a few sample generators converted. Phase two
converted the entire existing catalog — scenes, subjects, fragments, styles, and the
built-in prompt engines — to DPL, keeping pure-language files where possible and JS
sidecars where needed. Phase three wired DPL into the live engine and both loaders and
made the new v3 catalog the default, with the frozen v1 and v2 generations still fully
functional and addressed by a path prefix. Phase four added the wrapper UI — a
start/end frame applied around every prompt, with a sensible default distilled from the
most common endings in the old catalog — and reconciled the web app's building-block
panel so each generation browses the same way. The "full versus partial prompt"
distinction that drove a lot of duplication in the old system is on its way out, which
was the underlying goal all along.
