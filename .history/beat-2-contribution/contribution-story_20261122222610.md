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

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
### Issue Selection Toolkit

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

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

**Toolkit**

- Tool: `issue-scout` (`search-strategy.md`, `scope.md`, and `rubric.md`), run via `claude "issue-scout: run a scan"` and `claude "issue-scout: grade https://github.com/EdgeTX/edgetx/issues/1067 https://github.com/catalyst-cooperative/pudl/issues/3125"` on my Issue Selection site picks.
- What it produced: A 5-issue CLI scan saved in `scan-output.md` plus graded verdicts on my 2 picks, ending with `accept` and an `ambitious` difficulty note on `EdgeTX/edgetx#1067` (and `reject` on `catalyst-cooperative/pudl#3125`, closed as already fixed).
- Difficulties: My original Unit 1 `Newcomer Scope` check was calibrated for tidy sandbox issues and treated normal real-world issue complexity as a failure, and the scout could not measure local setup friction from the issue text alone.
- What changed: Replaced `Newcomer Scope` in `~/.claude/skills/issue-scout/rubric.md` with the `scope-feasible` check and difficulty-note instructions, logged the change with a date in `scan-notes.md`, and re-graded my picks before choosing `EdgeTX/edgetx#1067`.

---

## Understanding the Issue

### Problem Description

[In your own words, what is broken or missing?]

### Expected Behavior

[What should happen?]

### Current Behavior

[What actually happens?]

### Affected Components

[Which parts of the codebase are involved?]

### Toolkit

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

### Environment Setup

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

### Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

### Toolkit

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

### Root-Cause Analysis

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

### Proposed Solution

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

### Implementation Plan

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

### Toolkit

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

### Toolkit

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

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
