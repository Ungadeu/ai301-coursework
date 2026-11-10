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

## Branch

(<https://github.com/Ungadeu/fix-issue-64-check>)

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

### Run history

- Final run: 20/20, meets all criteria

### Package analysis

#### Check rationale

### Trade-offs

This check assumes all commented-out code is debris. If a PR intentionally comments out code to document an alternative approach, it will be falsely rejected. I verified this by running `--only` on the `unreviewable` category, confirming the strict threshold caught real debris without flagging clean PRs.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
