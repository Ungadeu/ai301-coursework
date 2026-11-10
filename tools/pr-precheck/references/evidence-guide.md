# Evidence guide: where evidence lives in a PR package

For each family: where to look in a practice package (eval mode), where
to look for my own PR (live mode), and what good looks like. Examples
come from `calib-01` (delta#2211, duplicate theme key) and my Unit 3
plan for zxlive#555.

## Plan fidelity (harness category: silent-drift)

- **Eval package:** `## Plan context`: the plan's `Files:` line, its
  "Not in scope" boundary, and any deviation note. Read it against
  `### Diff` (the changed file paths and hunks) and `### Description`
  (what the PR claims it does). In calib-01 the plan names
  `themes.gitconfig` only, says "Not in scope: any other theme", and
  says to remove the first, shadowed line.
- **My PR:** `plan.md` sections `## 2. Scope` (in scope plus the "Not
  in scope (boundary)" list), `## 3. Files to Touch`, and
  `## Deviations`; read against `git diff <default-branch>...HEAD`
  (three dots; for zxlive the default branch is `master`) and my draft
  PR title and description (`pr_draft.md`).
- **What good looks like:** every changed file appears in the plan's
  files list or a deviation note, every planned change appears in the
  diff, and nothing in the diff crosses the stated boundary. The
  description claims exactly what the diff does. calib-01 passes: one
  file, one removed line (the `#434C5E` one, as planned), and the
  description matches it. Silent drift goes in either direction: the
  diff does more than the plan (an extra file or refactor with no
  deviation note), or less (a planned step missing and not
  mentioned), or the description claims something the diff doesn't
  contain. A mismatch the PR states openly as a deviation, with a
  reason, is not drift.

## Test evidence (harness category: not-tested)

- **Eval package:** `### Test evidence`, read against the plan's
  `Test plan:` and the repro evidence in `## Plan context`, plus the
  test ask in `## Repo facts`. In calib-01 the plan's test plan is
  "re-run the configparser repro, expect a clean parse" and a
  `--show-syntax-themes` smoke check.
- **My PR:** `plan.md` `## 5. Test Plan` (the repro command with its
  expected before and after, plus the repo's CI checks) against the
  "Test plan results" I recorded under `## Deviations`, or my captured
  `test_evidence.md`; the repo's own checks come from its CI config
  and `CONTRIBUTING.md` (for zxlive: `pytest test/`, `mypy zxlive`,
  `ruff check`, `complexipy`).
- **What good looks like:** the evidence re-runs the issue's own
  failing scenario and shows an observable before and after, with the
  after matching the plan's expected-after. Where the repo asks for a
  test suite or checks, it names each command and its result (one line
  each is enough). calib-01 passes: the same configparser command
  shows the `DuplicateOptionError` before and `parsed OK` after, and
  `git config --get-all` shows one value, the same effective value as
  before. Not good: "works now", "all tests pass" with no output, or a
  test that only covers a case where the bug never happens. A step
  that wasn't run but is disclosed (like my manual GUI check in
  Deviation 4) is honest, as long as the issue's own scenario is
  still shown.

## Diff quality (harness category: unreviewable)

- **Eval package:** `### Diff` (the unified diff, every `+` and `-`
  line) and `### Commits` (the commit list and messages).
- **My PR:** `git diff <default-branch>...HEAD` and
  `git log <default-branch>..HEAD --oneline` on my branch (for zxlive,
  `fix/555-generated-rule-previews`); also `git status` to catch files
  I didn't mean to stage.
- **What good looks like:** every hunk is part of the fix or its
  tests, so a reviewer sees the change and nothing else. calib-01's
  diff is one removed line plus context, in one commit with a message
  that says what it does. Debris to look for: debug prints and logging
  left in, commented-out code, TODO scaffolding, whitespace or
  reformatting churn, edits to unrelated files, and local workarounds
  that slipped in (I kept my `conftest.py` patch off the branch, per
  Deviation 3).

## Standards and comms (harness category: standards-wall)

- **Eval package:** `## Repo facts`: the `pull requests:` line
  (template sections and asks) and the `contribution policy` line
  (including any AI-use rule); plus `## Thread highlights` for
  maintainer direction. Read them against `### Title` and
  `### Description`. calib-01 has no PR template, asks that PRs "stay
  small and reference the issue", and states no AI policy.
- **My PR:** the target repo's `.github/PULL_REQUEST_TEMPLATE.md` and
  `CONTRIBUTING.md` (and any AI policy file), plus maintainer comments
  on the issue thread; read against my draft title and description in
  `pr_draft.md`.
- **What good looks like:** every ask the repo states is met with real
  content: each template section filled (not left as placeholder
  text), the issue referenced (e.g. `Closes #555`), AI use disclosed
  when the policy asks for it, and any direction a maintainer gave in
  the thread followed. calib-01 passes: a small PR, and the
  description references #2211. Silence passes: if the repo asks for
  nothing, there is nothing to miss. Whether the description's claims
  match the diff is checked under plan fidelity, not here.
