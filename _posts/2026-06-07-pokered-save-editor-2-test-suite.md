---
title: "Pokered Save Editor 2: a test suite, and the save-corruption bug it caught"
subtitle: "An automated QtTest/CTest suite goes in — and immediately turns up an off-by-one that was clobbering a byte on every save."
date: 2026-06-07
tags: [pokered-save-editor-2, update]
---

A comprehensive automated test suite now covers
[Pokered Save Editor 2](https://github.com/junebug12851/pokered-save-editor-2),
built on QtTest and CTest. It exercises the save-file engine (fields, Pokémon,
items, world state, error handling, and full round-trips), the game database, and
the randomiser. To make the application logic testable in the first place, that
logic was extracted into a standalone `appcore` library, so the UI's models can now
be unit-tested rather than only exercised by hand.

The suite earned its keep on the first day. It found a save-corruption bug: the
checksum for the second bank of PC boxes was being written one byte early, which
also overwrote the last data byte of Box 6 on every save of a progressed file. With
the off-by-one corrected, a real save now round-trips byte-for-byte. This is exactly
the class of bug that is nearly impossible to notice by eye and trivial for a
round-trip test to catch — and it is the kind this editor cares about most, since
its core promise is to change only the exact bytes an edit requires and leave
everything else untouched.

A second find was a crash in the Day Care teardown when the Day Care was empty,
caused by an unconditional cleanup of a pointer that could be null. It was masked in
normal use but surfaced immediately under test.

The randomiser also reached the point of running end to end with test coverage for
its current scope, including invariants checked across repeated runs and byte
fidelity on the results. Features that aren't built yet — map and Hall of Fame
randomisation among them — are explicitly held back with re-enable notes rather than
left half-wired.
