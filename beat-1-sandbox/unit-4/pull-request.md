# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

### Pull request

Not opened yet. As of 2026-11-23 I have no pull request on `codepath/pathreview-ai301-fa26-s1` for issue #64; this field gets the PR's URL once it is open.

## Branch

Not pushed yet. My fork `Ungadeu/fix-issue-64-check` has a branch `Ungadeu/issue-64`, but it is 0 commits ahead of upstream `main`, so it holds no fix to review.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

### Run history

Full runs of `run_eval.py --skill tools/pr-precheck` that I have a transcript for, in order:

- 2026-11-23 (committed as `eval-run.txt`, Sonnet, 20 scored packages):

```text
categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

Earlier tuning runs during Unit 4 weren't saved, so their exact `agreement:` lines aren't recorded here.

### Package analysis

**pkg-07** (category `not-tested`). My rubric's verdict: `reject`. Gold label: `reject`. They agree, in the full run and in a single-package re-run (`--only pkg-07`) that I used to read the check grades:

- `matches-plan`: **pass**. "Diff touches only pkg/goanalysis/runner_fix.go and runner_fix_test.go, matching the plan's 'fix application code under pkg/goanalysis/, tests beside it'".
- `no-silent-drift`: **pass**. "All hunks are the grouping change, the unresolvable-position warning, or a test; the description claims exactly this".
- `test-evidence-present`: **fail**. "Evidence is 'Verified the fix on a single-file case' (./onefile/), the plan's control; the two-file a.go/b.go repro with go build ./... is never run".
- `unreviewable-debris`: **pass**. "No debug prints, TODOs or commented-out code in the diff".
- `standards-wall`: **pass**. "Repo asks for a brief description and states no AI policy".

So the code itself is fine, but the evidence only re-runs the single-file control case, where the bug never happens. The bug needs two files in one package. My `test-evidence-present` row requires the issue's own failing scenario, "not a narrower or easier case", so that one required failure makes the verdict `reject`.

#### Check rationale

From `tools/pr-precheck/rubric.md`:

> | **test-evidence-present** | `test_evidence` read against the plan's test plan and the issue's reproduction; `repo_facts` for the repo's stated test ask | `test_evidence` re-runs the issue's failing scenario (the same conditions the issue and plan describe, not a narrower or easier case) and shows an observable after-state matching the plan's expected-after; AND, if the repo asks for its suite or checks to pass, the evidence names that command and its outcome (a one-line stated result is enough; full logs are not required). Fails on a bare claim with no observable output ("works now", "verified on my machine", "all tests pass" alone) or on evidence that only exercises a case the bug does not occur in. A shortfall the PR openly discloses does not fail this check if the issue's scenario is still shown. | required |

Each clause exists for a specific failure:

- **"Not a narrower or easier case".** The `not-tested` packages show passing output from a case the bug never hits, like `pkg-07`'s single-file control. A check that only asked for "test output present" would pass them.
- **"A one-line stated result is enough".** This stops the check from rejecting good PRs just because they summarize the suite run instead of pasting full logs.
- **"A shortfall the PR openly discloses does not fail"**. This keeps an honest PR, one that shows the issue's scenario and says what it couldn't run, from scoring the same as one that hides the gap.

### Trade-offs

My `unreviewable-debris` row passes only if "The diff contains NO commented-out code, debug print statements, or accidental leftover scaffolding." That treats all commented-out code as debris. A PR that comments out an alternative implementation on purpose, to document it for reviewers, would be falsely rejected. I accept that edge case because silent debris is far more common than intentional commented-out examples. On 2026-11-23 I ran `--only pkg-12,pkg-15,pkg-18,pkg-02` as a canary. All three `unreviewable` packages failed this check on real debris (`// TODO: ring buffer?`, `eprintln!("DEBUG accept err = ...")`, a commented-out `eprintln!`), and the clean `clear-accept` package `pkg-02` passed it (`agreement: 4/4 scored items`).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
