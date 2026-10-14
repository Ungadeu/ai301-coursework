# Procedure: how this tool grades a PR package

## Read order

1. Read `scope.md` (in live mode only) to ensure the target matches.
2. Read `rubric.md`, `references/evidence-guide.md`, and `voice-guide.md`.
3. Read the `plan`, `pr_description`, and `repo_facts`.
4. Read the `test_evidence` and the `diff`.

## Evidence gathering

1. Extract the listed target files and intended logic changes from the `plan`.
2. Extract the actual changed files and lines of code from the `diff`.
3. Extract the terminal output and test results from `test_evidence`.
4. Extract the repo's formatting rules, PR template requirements, and AI disclosure rules from `repo_facts`.

## Check execution

1. For `matches-plan` and `no-silent-drift`, compare the `diff` side-by-side with the `plan`. If the diff alters files or adds functions not mentioned in the plan (without a Deviation note), grade as `fail`. 
2. For `test-evidence-present`, first note the failing scenario from the issue and the expected-after from the plan's test plan. Then read `test_evidence`: grade `pass` if it re-runs that same scenario with observable output matching the expected-after and, where `repo_facts` asks for the suite or checks, names the command and its result in at least one line. Grade `fail` if it only claims success ("works now", "all tests pass") without observable output, or if the scenario it runs is narrower than the one the bug occurs in (e.g. one file when the bug needs two).
3. For `unreviewable-debris`, scan the `diff`. If you see `print("here")`, `// TODO`, or large chunks of commented code, grade as `fail`.
4. For `standards-wall`, compare `pr_description` against `repo_facts`. If AI disclosure is required but missing, grade as `fail`.

## Verdict assembly

1. Treat any `unclear` grade on a `required` check as `fail`.
2. If all `required` checks are `pass`, output `accept`.
3. If any `required` check is `fail`, output `reject`. 
4. Output the human-readable summary, followed by the exact fenced JSON block format.
