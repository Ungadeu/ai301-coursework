# Contribution: Make the default setting for curves Y = X instead of Y = 0

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Uriel Ngadeu
**GitHub Username:** Ungadeu
**Issue:** <https://github.com/EdgeTX/edgetx/issues/1067>
**Pull Request:** <https://github.com/EdgeTX/edgetx/pull/8112>

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

### Unit 5: Upgraded issue-select into issue-scout and tuned CLI search filters

I installed `issue-scout` over my Unit 1 `issue-select` skill, copied my fit profile into `scope.md`, and wrote `search-strategy.md` with open-issue `gh search issues` queries (`--state open --limit 100`, sorted with `--sort updated` and dropping anything not updated in 60 days) to scan 5 live issues and grade 2 picks (`EdgeTX/edgetx#1067` and `catalyst-cooperative/pudl#3125`) from the AI301 Issue Selection site. During my first scan on 2026-11-08, the scout accepted 3 of the 5 scanned issues, but none was safe to take. My old `Newcomer Scope` check rejected workable real-world issues just for being messy, and `pudl#3125`, already closed as fixed in `#3737`, was rejected only because `Unclaimed Status` happened to catch it, since my rubric had no "issue is still open" check. Because of that, I replaced `Newcomer Scope` with a `scope-feasible` check, reworded `Unclaimed Status` for real repos on 2026-11-11 so any recent active claim blocks a pick, and logged both changes in `scan-notes.md`.

### Unit 6: Installed voice-guard hook, wild scopes, and repo memory file

I installed `voice-guard` into `~/.claude/voice-guard/`, merged an `## Upstream` section (Claims, Questions, and Pings rules) into my canonical `voice-guide.md` after noticing I had first written those rules only in the starter template the guard never reads, swapped the wild-repo `scope.md` files into `repro-check` and `plan-check`, and created `CLAUDE.local.md` in my clone of `Ungadeu/edgetx` (kept out of my PR via `.git/info/exclude`) so Claude remembers the curve subsystem and the `tests-radio` build commands. When I ran the wiring test (`gh issue comment --help`), the hook fired but logged `pass-through: help lookup, no body` instead of blocking, so I confirmed the stop with a body-less `gh issue comment` instead, which the guard blocked with "no body the guard can read". The guard then stopped my first EdgeTX claim draft under my own "Show what I tried and ask one clear question" rule, because it asked the maintainers to choose between Y = X and hiding undefined curves without naming anything I had checked. Because of that, I read `applyCustomCurve()` and `isCurveUsed()` in `radio/src/curves.cpp`, rewrote the claim to cite them before asking one either/or question, and only then got a guard pass and a repro-check `accept`.

### Unit 7: Installed the ship-gate and wrote an EdgeTX ship manifest

I installed the ship-gate (`python3 skill/install.py --repo ~/Desktop/edgetx`), which swapped pr-precheck to the scope for real repos. I filled `ship-manifest.md` with three checks from EdgeTX's CI: `gtests-radio` (the `tests-radio` target `build_fw.yml` runs through `tools/commit-tests.sh`), `check_radio_macros.py`, and `check_includes.py`. I moved `commit-tests.sh` and the hw_defs validator to the excluded table with dated reasons: a fresh configure can't find my pip-installed cmake, libc++ wrapper, or SDL2, and the validator fails at import on a missing `typing_extensions`. I expected my Unit 4 rubric might demand Path Review's `make` checks, but its `test-evidence-present` row was already repo-agnostic ("if the repo asks for its suite or checks to pass"), so it passed EdgeTX's C++ evidence unchanged. What actually fought me came in two parts. First, my first hand run of `check_gate.py` stopped on `standards-wall`, because @gagarinlg had answered "Probably both" on #1067 after I drafted, and my `Fixes #1067` claimed the whole issue while my description treated the picker filter as an either/or alternative. Second, opening the PR from a Claude session started in my course folder was stopped because the hook checks the session's start folder, not my clone. Because of that, I re-scoped the PR to "part of #1067", amended my commit message so merging won't auto-close the issue, and recorded the split in `plan.md` (plan-check went from reject back to accept). Then `check_gate.py` printed `ship-gate: PASS`, and I opened PR #8112 from a session inside `~/Desktop/edgetx`, where the hook honored that manual pass.

### Unit 8: Installed pr-monitor and wrote an EdgeTX review playbook

I installed `pr-monitor` into `~/.claude/pr-monitor/` and wrote `playbook.md` with response rules, EdgeTX staleness thresholds measured from five recent merged outside-contributor PRs, single-nudge etiquette aligned with my Unit 6 voice guide, and walk-away criteria. Running `monitor.py` on branch `fix/1067-default-curves-linear` read PR `#8112`'s live state (`<e.g., QUIET, under a day since opening, checks status>`) and drafted `<e.g., a wait note citing my X-day threshold / a review reply>`, so I `<e.g., kept the wait note off the GitHub thread rather than nudging early / rewrote the reply in my-reply.md and posted it through voice-guard>`. `<Name "Initially "Nothing --state EdgeTX/edgetx" I NEW NOTHING OR a all and at broke: confirmed confused drafted-move.md." fell for fork four free gh my or playbook pointed repo returned run second sections set-default short touching until verified what without you—e.g.,>` Because of that, `<state what you changed, or "I left the playbook thresholds as written and will re-run the monitor when new activity lands on #8112">`.

---

## Why I Chose This Issue

I sourced my candidate issues from the AI301 Issue Selection site. My `issue-scout` tool graded 2 picks: `EdgeTX/edgetx#1067` and `catalyst-cooperative/pudl#3125`. After patching my rubric's scope check in Unit 6, `issue-scout` gave my chosen issue (`EdgeTX/edgetx#1067`) a verdict of `accept` with an `ambitious` difficulty note, because maintainers never settled whether undefined curves should default to Y = X or be hidden from the curve picker; it rejected `pudl#3125` because a maintainer closed it as already fixed in #3737. I chose EdgeTX#1067 because nobody had an active claim on it (no assignee, no open PR, and a maintainer's 2021 offer to look at it never led anywhere), EdgeTX states no AI policy and has no `CONTRIBUTING.md`, so silence passes, and I want to learn how the radio firmware's mixer evaluates custom curves (`applyCustomCurve()` and `isCurveUsed()` in `radio/src/curves.cpp`) and how its `gtests-radio` harness tests that code. It is a stretch for me: the work is C++ firmware, not Python backend, and the scout's preferred `Technical Fit` check failed it for that reason.

Looking honestly at `issue-scout`, the tool was strong at checking repo liveness and claim status, but before the Unit 6 patch its sandbox-era scope check (`Newcomer Scope`) was too rigid and rejected viable real-world issues whose descriptions weren't textbook tidy. Replacing that row with `scope-feasible` and adding difficulty notes fixed the false rejections, though the scout still cannot judge how messy local environment setup will be until I clone the repo myself: reproducing EdgeTX#1067 took a pip-installed `cmake`, a compiler wrapper for my broken Command Line Tools headers, and building SDL2 from source. Its `Technical Fit` row is also stale (it still checks for "Python, Streamlit, or ChromaDB"), and it has no "issue is still open" check, so `pudl#3125` only failed because `Unclaimed Status` happened to catch the closed state.

**Claim comment:** <https://github.com/EdgeTX/edgetx/issues/1067#issuecomment-7089359024>

### Toolkit

- Tool: `issue-scout` (`search-strategy.md`, `scope.md`, and `rubric.md`), run via `claude "issue-scout: run a scan"` and `claude "issue-scout: grade https://github.com/EdgeTX/edgetx/issues/1067 https://github.com/catalyst-cooperative/pudl/issues/3125"` on my Issue Selection site picks.
- What it produced: A 5-issue CLI scan saved in `scan-output.md` plus graded verdicts on my 2 picks, ending with `accept` and an `ambitious` difficulty note on `EdgeTX/edgetx#1067` (and `reject` on `catalyst-cooperative/pudl#3125`, closed as already fixed).
- Difficulties: My original Unit 1 `Newcomer Scope` check was calibrated for tidy sandbox issues and treated normal real-world issue complexity as a failure, and the scout could not measure local setup friction from the issue text alone.
- What changed: Replaced `Newcomer Scope` in `~/.claude/skills/issue-scout/rubric.md` with the `scope-feasible` check and difficulty-note instructions, logged the change with a date in `scan-notes.md`, and re-graded my picks before choosing `EdgeTX/edgetx#1067`.

---

## Understanding the Issue

### Problem Description

When a user assigns an undefined (never-edited) custom curve such as `CV1` to an input or mixer line in EdgeTX, the firmware evaluates that curve as a flat `Y = 0` output across the entire stick travel instead of passing the input through linearly (`Y = X`). This causes the affected control channel (such as throttle) to stay stuck at zero until the user manually configures the curve.

### Expected Behavior

Assigning a newly selected or unconfigured custom curve should either default to a linear `Y = X` response (so stick input passes through predictably from `-1024` to `+1024`) or prevent unconfigured curves from silently zeroing out a channel.

### Current Behavior

An undefined custom curve has all-zero point values (`isCurveUsed()` returns `0`). When `applyCustomCurve()` passes those all-zero points to `intpol()`, every stick position (`-1024`, `0`, `+1024`) evaluates to `0`.

### Affected Components

- `radio/src/curves.cpp` (`applyCustomCurve()`, `intpol()`, and `isCurveUsed()`)
- `gui/colorlcd/controls/curve_param.cpp` (`CurveChoice` picker, discussed as an alternative approach in the issue thread)
- `radio/src/tests/mixer.cpp` (existing curve interpolation unit tests, including `TEST(Curves, LinearIntpol)`)

### Toolkit

- Tool: `CLAUDE.local.md` and Claude Code read-only exploration on my local `EdgeTX/edgetx` clone.
- What it produced: Confirmed the exact runtime path (`applyCustomCurve()` -> `intpol()` in `radio/src/curves.cpp`), the undefined-curve detector (`isCurveUsed()`), and the existing curve test location (`TEST(Curves, LinearIntpol)` in `radio/src/tests/mixer.cpp`).
- Difficulties: EdgeTX has no root `CONTRIBUTING.md`, `CLAUDE.md`, or `AGENTS.md`, and issue `#1067` contained two competing design ideas (defaulting to `Y = X` vs. hiding unused curves in the GUI picker).
- What changed: Documented the exact subsystem files, test target, and open design question in `CLAUDE.local.md` and asked maintainers about the preferred direction in my Unit 6 claim comment before writing code.

---

## Reproduction Process

#### Environment Setup

- **OS:** macOS 26.6.2 on an Intel (x86_64) MacBook Pro
- **Language / Runtime & Build Tools:** C++ (EdgeTX radio firmware) compiled with Apple clang 21.0.0; CMake 4.4.5 and Ninja 1.13.2 installed with pip 25.3 into a Python 3.14.3 venv, which also holds the build's code-generation deps from `pyproject.toml`; SDL2 2.32.10 built from source
- **Project Version / Commit:** `EdgeTX/edgetx` cloned from my fork at commit `8d79d2659` (upstream `main`, 2026-11-20)
- **Setup Commands:**
  1. `git clone https://github.com/Ungadeu/edgetx.git && cd edgetx && git remote add upstream https://github.com/EdgeTX/edgetx.git && git submodule update --init --recursive`
  2. `python3 -m venv .venv && .venv/bin/pip install cmake ninja asciitree clang jinja2 lz4 pillow pydantic pyelftools typing_extensions`
- **Setup Challenges:** Getting a test binary built took most of the effort, and none of it was EdgeTX's fault:
  - Homebrew no longer ships prebuilt bottles for Intel Macs and failed to build `cmake` from source, so I installed `cmake` and `ninja` from PyPI into the venv instead.
  - My Command Line Tools install has an incomplete `usr/include/c++/v1` (even a one-line `#include <cstddef>` fails), so I compiled through a small wrapper that passes `-stdlib++-isystem` pointing at the SDK's libc++ headers, and set `CPLUS_INCLUDE_PATH` for the libclang-based `datacopy` generator.
  - CMake picked up Anaconda's Python 3.9, which lacks `pydantic`, so the hardware headers (`hal_settings.h`) were never generated until I passed `-DPython3_EXECUTABLE` pointing at the venv.
  - The tests link against the simulator sources, which need SDL2, so I built SDL2 2.32.10 from source into `build/sdl2-install` and passed `-DSDL2_DIR`. I skipped Companion with `-DDISABLE_COMPANION=YES` because it needs Qt 6, which the unit tests don't use.

#### Steps to Reproduce

1. Add a gtest at `radio/src/tests/repro_1067.cpp` (picked up by the `tests/` CMake glob) that uses the default model, applies never-defined custom curve CV1 to the throttle input (`expo->curve.type = CURVE_REF_CUSTOM; expo->curve.value = makeSourceNumVal(1);`), and prints the throttle channel output at stick positions −1024, 0, and +1024, first with no curve as a control and then with CV1. The full file is in my repro report.
2. Build and run it with the same targets CI uses in `tools/commit-tests.sh`: `cmake -G Ninja -DPCB=X10 -DPCBREV=TX16S -DCMAKE_BUILD_TYPE=Debug -DDISABLE_COMPANION=YES ../..`, then `cmake --build . --target native-configure`, `cmake --build native --target gtests-radio`, and `native/gtests-radio --gtest_filter='Repro1067Test.*'`.
3. Observed result: with no curve, the throttle channel follows the stick end to end (−1024 / 0 / +1024). With never-defined CV1 applied, the channel stays at 0 at every stick position, and `isCurveUsed(0)` returns 0. That is the flat Y = 0 the issue describes for an undefined curve.

### Reproduction Evidence

- **Commit showing reproduction:** none. The repro test is local only (untracked in my clone) and is not meant for the PR; its full source is in my repro report.
- **Claim comment:** https://github.com/EdgeTX/edgetx/issues/1067#issuecomment-7089359024
- **Repro comment:** pending (drafted in `repro-draft.md`, graded `accept` by repro-check, not yet posted)
- **Screenshots/logs:**

$ native/gtests-radio --gtest_filter='Repro1067Test.*'
############ Running 1 test(s) from 1 test case(s), iteration: 1.
[----------] 1 test from Repro1067Test
[repro-1067] isCurveUsed(0) [CV1] = 0
[repro-1067] no curve      stick=-1024 -> THR channel=-1024
[repro-1067] no curve      stick=0 -> THR channel=0
[repro-1067] no curve      stick=1024 -> THR channel=1024
[repro-1067] CV1 undefined stick=-1024 -> THR channel=0
[repro-1067] CV1 undefined stick=0 -> THR channel=0
[repro-1067] CV1 undefined stick=1024 -> THR channel=0
+
[==========] 1 test from 1 test suite ran (0 ms total)
[  PASSED  ] 1 test.

- **My findings:** The bug reproduces on current `main`. The code path matches what I read before claiming: `applyCustomCurve()` in `radio/src/curves.cpp` sends a curve with all-zero points to `intpol()`, which returns 0, and `isCurveUsed()` already identifies such a curve as undefined. I reproduced it through the firmware's own unit-test harness rather than on a physical radio or the GUI simulator, and my report says so.

### Toolkit: Reproduction

- Tool: `repro-check` (my rubric, evidence guide, and the wild `scope.md`), run via `claude "repro-check: grade my claim comment in claim-draft.md and my repro report in repro-draft.md for issue https://github.com/EdgeTX/edgetx/issues/1067"`, with `voice-guard` checking both drafts first via `check_voice.py --draft`.
- What it produced: `accept`, with all five required checks passing (Claim Intent, Environment Record, Followable Steps, Behavior Match, AI Disclosure).
- Difficulties: Running it headless with `claude -p`, it couldn't approve `gh` calls or read `~/.claude/skills/`, so I re-ran it with `--add-dir` and read-only `gh` permissions. It caught a real flaw: my pasted output said `2 tests` while the command shown filtered to one, because I had run it with an extra `Curves.*` filter. It also warned that my claim was already posted, so posting `claim-draft.md` again would be a duplicate claim.
- What changed: I re-ran the test with exactly the documented command and pasted that real output (`1 test`) into `repro-draft.md`, and I'm posting only the repro comment, not a second claim.

---

## Solution Approach

### Root-Cause Analysis

In `radio/src/curves.cpp`, `applyCustomCurve(int x, int8_t idx)` looks up the curve definition and passes its stored control points to `intpol()`. Because an unconfigured curve initializes all points to `0`, `intpol()` returns `0` for every stick position `x`. Meanwhile, `isCurveUsed()` in `radio/src/curves.cpp` already detects whether a custom curve has been configured (`0` when all points are zero and the curve has no custom configuration).

### Proposed Solution

Update `applyCustomCurve()` in `radio/src/curves.cpp` so that when `isCurveUsed()` indicates the referenced custom curve is unconfigured, it returns the input value `x` directly (`Y = X` linear passthrough) rather than interpolating all-zero points into `Y = 0`. Add a unit test next to `TEST(Curves, LinearIntpol)` in `radio/src/tests/mixer.cpp` verifying that an undefined custom curve outputs `-1024`, `0`, and `+1024` for those stick inputs while configured curves keep their exact existing behavior.

### Implementation Plan

1. Inspect `applyCustomCurve()` and `isCurveUsed()` in `radio/src/curves.cpp` (confirming 0-based vs. 1-based curve indexing and negative/inverted curve indices like `-CV1`).
2. Update `applyCustomCurve()` in `radio/src/curves.cpp` to return `x` (or `-x` for inverted references, matching existing sign handling) when the referenced curve is unused.
3. Add a focused unit test in `radio/src/tests/mixer.cpp` next to `TEST(Curves, LinearIntpol)` covering undefined curve passthrough and ensuring configured curves are unaffected.
4. Rebuild and run `gtests-radio` (plus the repro test) to verify the before/after change and zero regressions.

Deviation (recorded in `plan.md`): after `@gagarinlg` replied "Probably both" on `#1067`, I scoped PR `#8112` to "part of #1067", leaving the `CurveChoice` picker filter for a follow-up, and wrote the fixture-based check as a separate `TEST_F(MixerTest, ...)`.

### Toolkit

- Tool: `plan-check` (my rubric, procedure, evidence guide, and the wild `scope.md`), run via `claude "plan-check: grade my plan in plan.md and draft comment in plan-comment.md for issue https://github.com/EdgeTX/edgetx/issues/1067"` with read-only `gh` permissions.
- What it produced: `reject` first (no `plan.md`), then `accept` with all five required checks passing (diagnosis-grounded, bounded-scope, executable-by-a-stranger, test-decisive, comment-faithful) and the preferred risk-awareness check passing.
- Difficulties: it caught real gaps in my plan. My repro test asserts `== 0`, so it would fail after the fix. My comment overstated "defined curves stay unchanged". It also found I'd missed a caller (`applyCurrentCurve()` at `curves.cpp:417`). It flagged procedure gaps too: my `procedure.md` and evidence guide look for `comment.md` instead of `plan-comment.md`, the evidence guide still mentions the Path Review repo and has empty template sections, and nothing says what to do when no repro comment is posted.
- What changed: I wrote the expected repro failure into the test plan, added the flat-curve trade-off and the real test name to the comment, added the missing caller to Risks, and re-graded to `accept`. The skill-file gaps are still to fix.

---

## Testing Strategy

I proved the fix with three observable checks, all run from `build/repro` against the TX16S configure CI uses (`-DPCB=X10 -DPCBREV=TX16S`). Full logs are in my local `test_evidence.md`.

1. **Before/after repro check.** I re-ran my Unit 6 repro (`native/gtests-radio --gtest_filter='Repro1067Test.*:Curves.*'`) before and after the change. Before: with never-defined CV1 on the throttle input, the channel read `0 / 0 / 0` at stick −1024 / 0 / +1024, while the no-curve control read `-1024 / 0 / 1024`. After: CV1 reads `-1024 / 0 / 1024`, identical to the control. The repro test now fails on purpose, because it asserts the old `0`, and that failure is the before/after proof.
2. **New regression tests that fail without the fix.** I added `Curves.UndefinedCurveIsIdentity` (calls `applyCustomCurve()` directly at −1024, 0, 1024 and −192) and `MixerTest.UndefinedCurveOnInputFollowsStick` (the same setup as my repro, asserting the channel follows the stick) to `radio/src/tests/mixer.cpp`. With only `curves.cpp` reverted, both fail (`Which is: 0`, expected `-1024`/`1024`), and the existing `Curves.LinearIntpol` still passes. With the fix, all three pass.
3. **Full `gtests-radio` suite.** On unchanged code: `291 tests ... PASSED` (290 upstream + my local repro). With the fix, and the repro file moved out of the source tree so it can't ship: `292 tests from 43 test suites ran ... [ PASSED ] 292 tests` (290 upstream + my 2 new tests). No existing test changed result.

My ship manifest's checks also pass in a fresh shell on commit `803f2a7ef`: `gtests-radio` (292/292), `tools/check_radio_macros.py` (OK), and `tools/check_includes.py` (exit 0). Not yet verified: a hands-on check in the radio simulator, which needs Qt 6.

### Toolkit

- Tool: the ship-gate (`~/.claude/ship-gate/check_gate.py` as a `PreToolUse` hook) with my `ship-manifest.md` in the clone, installed via `python3 skill/install.py --repo ~/Desktop/edgetx`.
- What it produced: a manifest with three must-pass checks taken from EdgeTX's CI (`build_fw.yml` → `tests-radio`, `validate_radio_macros.yml`, `validate_includes.yml`), all passing, plus a hook test where `gh pr create --help` was stopped with `ship-gate: STOP. no PR text to check`.
- Difficulties: the ship-gate runs each check in a fresh terminal without my venv, and EdgeTX's own `tools/commit-tests.sh` does a fresh `cmake` configure that can't find this Mac's pip-installed cmake, libc++ compiler wrapper, or locally built SDL2. The hw_defs validator also failed at import (`typing_extensions` missing). The install notes said the hook test should show two stops, but only the ship-gate's appeared, because my voice guard deliberately passes `--help` lookups.
- What changed: I wrote the test row with an explicit `.venv/bin` PATH and my existing `build/repro` configure (same `tests-radio` target as CI), and moved `commit-tests.sh` and the hw_defs check into the manifest's excluded table with dated reasons, instead of deleting them.

---

## Implementation Notes

**2026-11-22**

I installed the ship-gate and wrote my plan. My first `plan-check` run on #1067 was a `reject`, because I had only drafted `plan-comment.md` and `plan.md` didn't exist yet. I wrote `plan.md` (diagnosis with my repro output, an in/out scope list, the exact guard, a before/after test plan, and risks), and it passed. While listing risks, I grepped every caller of `applyCustomCurve()` and found it isn't only inputs and mixes: output curves (`mixer.cpp:310-312`) and the curve editors' previews and point resampling also call it, so they all change behavior for an undefined curve. I also wrote down that `isCurveUsed()` can't tell a never-defined curve from a 5-point curve someone zeroed on purpose.

**2026-11-23**

I created `fix/1067-default-curves-linear` from `main` (I confirmed it matched `upstream/main`) and re-ran my repro and the full suite before touching code, so the "before" numbers were fresh. The change is four lines in `applyCustomCurve()` in `radio/src/curves.cpp`: after the existing `idx >= MAX_CURVES` check, return `x` when `!isCurveUsed(idx)`. I added two tests next to `LinearIntpol` in `radio/src/tests/mixer.cpp`. Two decisions differed from the plan, and I recorded both in its Deviations section. The mixer-level check became its own `TEST_F(MixerTest, ...)`, because it needs the fixture. The commit scope became `fix(curves)` to match how EdgeTX scopes by subsystem. To prove the tests were real, I stashed only `curves.cpp` and confirmed both new tests fail without the fix. Then I moved `repro_1067.cpp` out of the source tree into the git-ignored `build/evidence/` so it can't land in the PR, and checked `git diff main...HEAD --stat` (only `curves.cpp` and `mixer.cpp`, 31 insertions). Commit: `803f2a7ef fix(curves): default undefined custom curves to linear Y = X`. The maintainer design question on the thread is still unanswered, so the branch is built but not pushed as a PR.

**2026-11-23 (PR opened)**

After `@gagarinlg` answered "Probably both" on `#1067`, I updated `plan.md` to scope this branch to the `Y = X` default only (`part of #1067` rather than `Fixes #1067`), amended the commit message so merging will not auto-close the issue, re-ran `plan-check` and `check_gate.py --branch` until `ship-gate: PASS`, pushed `fix/1067-default-curves-linear`, and opened PR `#8112` on `EdgeTX/edgetx` from inside `~/Desktop/edgetx`.

**Toolkit**

- Tool: Claude Code with `CLAUDE.local.md` (for C++ curve/test implementation) plus `plan-check` re-run after re-scoping `#1067`.
- What it produced: A 4-line `!isCurveUsed(idx)` guard in `radio/src/curves.cpp`, two regression tests (`Curves.UndefinedCurveIsIdentity` and `MixerTest.UndefinedCurveOnInputFollowsStick`) in `radio/src/tests/mixer.cpp`, and an `accept` verdict from `plan-check` after updating `plan.md`.
- Difficulties: When `@gagarinlg` answered "Probably both" mid-build, my first commit message (`Fixes #1067`) overclaimed the issue and would have auto-closed it before the picker-filter half was addressed; I also had to isolate `repro_1067.cpp` outside the tracked tree so it would not leak into the diff.
- What changed: Amended the commit and PR description to `"part of #1067"`, recorded both the scope split and the `TEST_F(MixerTest, ...)` fixture decision in `plan.md`'s Deviations section, moved `repro_1067.cpp` into git-ignored `build/evidence/`, and verified `git diff main...HEAD --stat` touched only `curves.cpp` and `mixer.cpp`.

---

## Pull Request

**PR Link:** <https://github.com/EdgeTX/edgetx/pull/8112>

**PR Description:** Addresses the `Y = X` firmware default half of `#1067` (`part of #1067`, leaving the `CurveChoice` picker filter for a separate change per `@gagarinlg`'s comment) by updating `applyCustomCurve()` in `radio/src/curves.cpp` so unconfigured custom curves return `x` instead of `0`, adds two regression unit tests in `radio/src/tests/mixer.cpp`, includes before/after `gtests-radio` output (`292/292` passing), and discloses Claude Code assistance.

**Maintainer Feedback:**

- 2026-11-23: none yet. The only comment is an automated MemBrowse memory report from `github-actions` (+8 to +104 B of flash per target), not a human review. `monitor.py` drafted a wait note, with the earliest nudge on 2026-11-30.

**Status:** Awaiting review (42 checks passing, mergeable, no review decision yet)

**Toolkit**

- Tool: `ship-gate` (`check_gate.py`, `ship-manifest.md`, and `pr-precheck` with `scope-live.md`) alongside `voice-guard`, run by hand with `check_gate.py --branch` and then through `claude "run this command: gh pr create ..."`.
- What it produced: Confirmed all three manifest checks passed (`gtests-radio`, `check_radio_macros.py`, `check_includes.py`), returned `pr-precheck` verdict `accept` and `ship-gate: PASS`, logged the fingerprints in `~/.claude/ship-gate/gate-log.md`, and allowed `gh pr create` to open PR `#8112` on `EdgeTX/edgetx`.
- Difficulties: My first manual `check_gate.py` run stopped on `standards-wall` because `@gagarinlg` had replied "Probably both" on `#1067` while my draft still said `Fixes #1067` and framed the picker filter as an either/or choice. Then my first `gh pr create` attempt stopped because I ran it from a Claude session started in my course folder instead of `~/Desktop/edgetx`.
- What changed: Re-scoped the PR and amended the commit message to `"part of #1067"`, updated `plan.md`, re-ran `check_gate.py --branch` to `ship-gate: PASS`, and opened PR `#8112` from a fresh Claude session inside `~/Desktop/edgetx` so the hook honored the manual pass.

---

## Learnings and Reflections

### Technical Skills Gained

Working on `EdgeTX/edgetx#1067` pushed me well beyond Python into a real C++ embedded radio firmware codebase. I learned how EdgeTX's mixer pipeline evaluates custom curves (`applyCustomCurve()`, `intpol()`, and `isCurveUsed()` in `radio/src/curves.cpp`), how to write and run targeted GoogleTest regression tests (`TEST` and `TEST_F(MixerTest, ...)`) inside the `gtests-radio` native harness, and how to diagnose complex cross-toolchain build issues on macOS Intel (pip-installed CMake/Ninja, libc++ header wrappers, libclang codegen paths, and building SDL2 from source). On the workflow side, I learned how to pair deterministic local checks (`ship-manifest.md`, `git diff main...HEAD`) with rubric-driven AI gates (`repro-check`, `plan-check`, `pr-precheck`, `voice-guard`, and `pr-monitor`).

### Challenges Overcome

Three real obstacles forced me to adapt rather than brute-force. First, getting `gtests-radio` to compile on macOS Intel took solving four stacked toolchain failures (broken Homebrew bottles, missing Command Line Tools C++ headers, Anaconda shadowing the venv Python, and missing SDL2). Second, my own `voice-guard` blocked my initial EdgeTX claim draft under my "Show what I tried" rule, forcing me to read `curves.cpp` before asking maintainers an informed either/or question—which directly paid off when `@gagarinlg` replied `"Probably both"`. Third, my first `ship-gate` run caught a real `standards-wall` mismatch between that maintainer reply and my `Fixes #1067` claim, pushing me to re-scope cleanly to `"part of #1067"` and verify the split with `plan-check` before opening PR `#8112`.

### What I'd Do Differently Next Time

Next time, I will audit my skill files whenever I switch repositories—my Unit 1 `Technical Fit` rubric row stayed pinned to Python/ChromaDB and `plan-check`'s evidence guide still referenced Path Review's `comment.md` filename. I would also check a repository's local build requirements and CI workflow files *before* finalizing my issue choice so toolchain surprises like Qt 6 or SDL2 don't consume half my setup window, and I would always start my Claude Code session directly inside the target repo clone so hooks resolve the right working directory on the first try.

---

## Resources Used

- [EdgeTX Issue #1067 — Make the default setting for curves Y = X instead of Y = 0](https://github.com/EdgeTX/edgetx/issues/1067) (issue context, prior discussion, and `@gagarinlg`'s `"Probably both"` design reply that shaped PR `#8112`'s scope)
- [EdgeTX Pull Request #8112](https://github.com/EdgeTX/edgetx/pull/8112) (my submitted fix, test evidence, and PR thread monitored by `pr-monitor`)
- [EdgeTX CI Test Script (`tools/commit-tests.sh`)](https://github.com/EdgeTX/edgetx/blob/main/tools/commit-tests.sh) and `.github/workflows/build_fw.yml` (source for the `TX16S` CMake flags, `gtests-radio` target, and `check_radio_macros.py` / `check_includes.py` checks in `ship-manifest.md`)
- [EdgeTX Curve Implementation (`radio/src/curves.cpp`)](https://github.com/EdgeTX/edgetx/blob/main/radio/src/curves.cpp) and [Mixer Unit Tests (`radio/src/tests/mixer.cpp`)](https://github.com/EdgeTX/edgetx/blob/main/radio/src/tests/mixer.cpp) (traced `applyCustomCurve()`, `isCurveUsed()`, and `TEST(Curves, LinearIntpol)`)
- [GitHub CLI (`gh`) Manual](https://cli.github.com/manual/) (used for `gh search issues`, `gh repo set-default`, `gh issue comment`, `gh pr create`, and `pr-monitor` state checks)
