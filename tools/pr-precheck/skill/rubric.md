# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
| :--- | :--- | :--- | :--- |
| **matches-plan** | `diff`, `plan` | Every file and code change in the diff is explicitly requested in the plan or its `Deviations` section. | required |
| **no-silent-drift** | `diff`, `plan`, `pr_description` | The diff contains NO unrelated changes, extra helper functions, or format churn that was not stated in the plan or explicitly disclosed in the PR description notes. | required |
| **test-evidence-present** | `test_evidence` read against the plan's test plan and the issue's reproduction; `repo_facts` for the repo's stated test ask | `test_evidence` re-runs the issue's failing scenario (the same conditions the issue and plan describe, not a narrower or easier case) and shows an observable after-state matching the plan's expected-after; AND, if the repo asks for its suite or checks to pass, the evidence names that command and its outcome (a one-line stated result is enough; full logs are not required). Fails on a bare claim with no observable output ("works now", "verified on my machine", "all tests pass" alone) or on evidence that only exercises a case the bug does not occur in. A shortfall the PR openly discloses does not fail this check if the issue's scenario is still shown. | required |
| **unreviewable-debris** | `diff` | The diff contains NO commented-out code, debug print statements, or accidental leftover scaffolding. | required |
| **standards-wall** | `pr_description`, `repo_facts` | The PR description accurately fills out every section of the repo's PR template and explicitly discloses AI assistance if the repo's `CONTRIBUTING.md` requires it. | required |

## Verdict rule

Output `accept` (ready) if every `required` check is `pass`. Output `reject` (hold) if any `required` check is `fail` or `unclear`. `unclear` counts as `fail`.
