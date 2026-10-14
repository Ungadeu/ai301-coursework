# Evidence guide: where evidence lives in a PR package

## 1. Candidate Plan (`plan`)

- **Where it lives:** `plan.md` in the local repo (Live), or `## Plan` in the bundle (Eval).
<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

## 2. PR Draft (`pr_description`)

- **Where it lives:** `pr_draft.md` in the local repo (Live), or `## PR description` (Eval).
- **What to look for:** A filled PR template, Closes #, checked testing boxes, and Notes for Reviewers containing AI disclosures.
- **What to look for:** The exact files and code edits promised, and the `Deviations` section.
<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

## Test evidence (harness category: not-tested)

## 3. Test Evidence (`test_evidence`)

- **Where it lives:** `test_evidence.md` (Live), or `## Test evidence` (Eval).
- **What to look for:** Raw terminal output proving the fix works, and the output of the repo's `make` commands.
<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

## Diff quality (harness category: unreviewable)

## 4. The Code Diff (`diff`)

- **Where it lives:** Generated via `git diff main...HEAD` (Live), or `## Diff` (Eval).
- **What to look for:** The exact lines of code added (`+`) or removed (`-`). It must perfectly match the plan without extra debris.
<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

## Standards and comms (harness category: standards-wall)

## 5. Repo Facts (`repo_facts`)

- **Where it lives:** Fetched from GitHub (Live), or `## Repo facts` (Eval).
- **What to look for:** The PR template structure and `CONTRIBUTING.md` policies.
<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->
