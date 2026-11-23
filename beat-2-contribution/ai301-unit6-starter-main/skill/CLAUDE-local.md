
# My notes on [repo] (local, never committed)

Repo: `EdgeTX/edgetx` (fork `Ungadeu/edgetx` cloned to `~/Desktop/edgetx`, `EdgeTX/edgetx` set as `upstream`) | Issue: `#1067` | Written: 2026-11-22

## Conventions from CONTRIBUTING.md

EdgeTX has no root `CONTRIBUTING.md`, `CLAUDE.md`, or `AGENTS.md`. These rules come from the PR template, `docs/contributing/`, and recent commits:

- **PR descriptions:** Include `Fixes #1067` and a clear summary of the change.
- **Commit titles:** Follow the `fix(scope): ...` format.
- **Design first:** Settle the open design question on issue `#1067` before writing implementation code.
- **Keep local files out of git:** `CLAUDE.local.md` is ignored via `.git/info/exclude` so it never enters a commit or PR.

## The subsystem my issue touches

- **Where `Y = 0` comes from:** `applyCustomCurve()` → `intpol()` in `radio/src/curves.cpp`.
- **Two candidate fix locations (pending issue discussion):** Either the `isCurveUsed()` check, or the `CurveChoice` curve picker in `gui/colorlcd/controls/curve_param.cpp`.
- **Where tests live:** `radio/src/tests/mixer.cpp` — place the new test right next to `TEST(Curves, LinearIntpol)`.

## Build and test commands

- **Initialize submodules first** (skipped during initial clone; required before building):

  ```bash
  git submodule update --init --recursive

## House style and stated AI policy

House style: Match surrounding C++ style in radio/src/ and gui/colorlcd/, keep changes scoped to #1067, and use fix(scope): ... commit titles.

AI policy: None stated. Follow course practice anyway: disclose AI assistance honestly, in my own words, in the PR description and any relevant upstream posts.
