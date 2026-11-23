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
**Pull Request:** [GitHub PR link — fill in during Part 3]

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

### Unit 5: issue-scout

- **Tool:** Upgraded issue-select into issue-scout and tuned CLI search filters
- **What it produced:** A ranked list of 5 open-source issues via CLI search, plus 2 graded picks from the AI301 Issue Selection site.
- **What fought me:** The initial search returned too many abandoned issues with no recent maintainer activity.
- **What I changed:** I installed `issue-scout` over my Unit 1 `issue-select` skill, copied my Python/backend fit profile into `scope.md`, and wrote `search-strategy.md` with open-issue `gh search issues` queries (`--state open --limit 100`) and ranking filters to scan 5 live issues and grade **[2 or 3]** picks from the AI301 Issue Selection site. During my first scan on **[Date from scan-notes.md]**, **[name one real thing that broke or fell short — e.g., "my initial query returned stale issues with no maintainer replies in over a year / a repo like `<repo-name>` failed my Maintainer Alive check because..."]**. Because of that, I **[state your real change — e.g., "added `--sort updated` and an unassigned filter in `search-strategy.md`, then logged the change in `scan-notes.md` so the top 5 results surfaced active Python repos"]**.

### Unit 6: Installed voice-guard hook, wild scopes, and repo memory file

I installed `voice-guard` into `~/.claude/voice-guard/`, merged an `## Upstream` section (Claims, Questions, and Pings rules) into my canonical `voice-guide.md` after noticing I had first written those rules only in the starter template the guard never reads, swapped the wild-repo `scope.md` files into `repro-check` and `plan-check`, and created `CLAUDE.local.md` in my clone of `Ungadeu/edgetx` (kept out of my PR via `.git/info/exclude`) so Claude remembers the curve subsystem and the `tests-radio` build commands. When I ran the wiring test (`gh issue comment --help`), the hook fired but logged `pass-through: help lookup, no body` instead of blocking, so I confirmed the stop with a body-less `gh issue comment` instead, which the guard blocked with "no body the guard can read". The guard then stopped my first EdgeTX claim draft under my own "Show what I tried and ask one clear question" rule, because it asked the maintainers to choose between Y = X and hiding undefined curves without naming anything I had checked. Because of that, I read `applyCustomCurve()` and `isCurveUsed()` in `radio/src/curves.cpp`, rewrote the claim to cite them before asking one either/or question, and only then got a guard pass and a repro-check `accept`.

### Unit 7: [one line on the tool work]

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

### Unit 8: [one line on the tool work]

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

```text
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
[==========] 1 test from 1 test suite ran. (0 ms total)
[  PASSED  ] 1 test.
```

- **My findings:** The bug reproduces on current `main`. The code path matches what I read before claiming: `applyCustomCurve()` in `radio/src/curves.cpp` sends a curve with all-zero points to `intpol()`, which returns 0, and `isCurveUsed()` already identifies such a curve as undefined. I reproduced it through the firmware's own unit-test harness rather than on a physical radio or the GUI simulator, and my report says so.

**Toolkit**

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

### Toolkit

- Tool:
- What it produced:
- Difficulties:
- What changed:

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

**Toolkit**

- Tool: `plan-check` (my rubric, procedure, evidence guide, and the wild `scope.md`), run via `claude "plan-check: grade my plan in plan.md and draft comment in plan-comment.md for issue https://github.com/EdgeTX/edgetx/issues/1067"` with read-only `gh` permissions.
- What it produced: `reject` first (no `plan.md`), then `accept` with all five required checks passing (diagnosis-grounded, bounded-scope, executable-by-a-stranger, test-decisive, comment-faithful) and the preferred risk-awareness check passing.
- Difficulties: it caught real gaps in my plan. My repro test asserts `== 0`, so it would fail after the fix. My comment overstated "defined curves stay unchanged". It also found I'd missed a caller (`applyCurrentCurve()` at `curves.cpp:417`). It flagged procedure gaps too: my `procedure.md` and evidence guide look for `comment.md` instead of `plan-comment.md`, the evidence guide still mentions the Path Review repo and has empty template sections, and nothing says what to do when no repro comment is posted.
- What changed: I wrote the expected repro failure into the test plan, added the flat-curve trade-off and the real test name to the comment, added the missing caller to Risks, and re-graded to `accept`. The skill-file gaps are still to fix.

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

### Technical Skills Gained

[What you learned technically, named concretely.]

### Challenges Overcome

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

### What I'd Do Differently Next Time

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
