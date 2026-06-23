---
title: "Random AI Prompt: a full test suite, and back to shipping"
subtitle: "Vitest and Playwright land, then a long-stalled CI pipeline is unbroken so the stable branch can move again."
date: 2026-06-22
tags: [random-ai-prompt, update]
---

[Random AI Prompt](https://github.com/junebug12851/random-ai-prompt) closed out its
revival sprint with the two things a modernised project needs most: real tests and a
working release path.

Until now the project had only linting and an import smoke test. It now has a
comprehensive suite. Vitest covers the Node side — unit, integration, snapshot,
contract, and regression tests — and the React app, with component tests and a
real-data integration test of the browser engine. Playwright builds the app and runs
end-to-end, visual-regression, and accessibility checks against the served build. The
result is 118 unit/integration tests and 8 browser specs, all green. A genuinely
tricky detail was documented along the way: the underlying utility library captures
the random function at import time, so tests can't simply stub randomness — they assert
invariants instead, and only the language's own seeded renderer is driven
deterministically. (Getting the browser tests to launch on the development machine was
its own saga, ultimately solved by pointing them at the system Chrome.)

With tests in place, the focus turned to shipping. The stable branch had been
deliberately held at the pre-revival state, and the recent commits were red in CI —
not from test failures, but because the lockfiles had drifted out of sync after the new
dependencies came in. The real fix was a clean, full dependency resolve so every
platform's optional packages are recorded, not an incremental update that omits the
Linux-only pieces. Formatting that CI had never gotten far enough to flag was also
cleaned up. Once green, the stable branch fast-forwarded to the current work for the
first time in the revival — which then exposed two more first-time deployment breakages
in the docs and release workflows, both fixed. A recurring theme of the week held true
to the end: the failures were almost never the code itself, but the build, packaging,
and tooling around it.
