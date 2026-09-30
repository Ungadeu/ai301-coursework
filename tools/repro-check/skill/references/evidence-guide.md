# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->
## Package parts

- **Claim comment**: eval bundle, the "Candidate claim comment" section.
  Live, the student's draft claim comment.
- **Repro report**: eval bundle, the "Candidate repro report" section
  (its result line, environment line, steps, output blocks, and
  expected/actual). Live, the student's draft repro comment.
- **Issue**: eval bundle, the "Issue" section (title, body, reported
  version and platform) plus "Thread highlights" (maintainer trigger
  notes, other confirmations and the versions they used). Live, the
  issue page and its comments.
- **Repo facts**: eval bundle, the "Repo facts" block: latest release,
  the bug-report template's asks, and the contribution policy
  (including any AI-use policy). Live, the repo's issue templates,
  `CONTRIBUTING.md`, and any `AI_POLICY.md`.

## Environment

- Where it lives: the "Environment:" line or block in the repro
  report. Compare it with the version and platform in the issue body,
  the versions in the thread highlights, the latest release in repo
  facts, and what the bug-report template asks for (e.g. "confirm on
  latest and main", "give your OS and driver").
- What good looks like: the OS and the tool's version are named, plus
  any runtime, driver, or shell the issue says matters. The version
  tested matches what the issue targets, or the report says how it
  differs ("issue is on 3.8.4, I tested 3.9.6"). Testing a much older
  release than the issue confirms, with no mention of the gap, is a
  silent deviation and fails. No environment record at all fails,
  however convincing the log looks.

## Steps

- Where it lives: the "Steps:" list or command block in the repro
  report, read against the trigger in the issue body and any trigger
  note from a maintainer in the thread highlights.
- What good looks like: a stranger could type them in order from an
  empty directory or a fresh install and reach the trigger. Every input
  file, config, and flag is shown or public. Fails: "our private
  monorepo", "our internal config (not shareable)", "ran our
  pre-commit hook", or steps that drop a condition the issue says is
  essential (the driver on a driver-specific issue, the flag the
  maintainer named as the trigger).

## Behavior shown

- Where it lives: the fenced output blocks, logs, tracebacks, and
  prompt captures in the repro report, and its "Expected / Actual"
  lines. Read them against the exact behavior the issue describes
  (error text, exit status, wrong output, crash vs. graceful error).
- What good looks like: the artifact came from the issue's own input
  or syntax and shows the issue's symptom. An adjacent symptom fails
  even when the report calls it a match: a different error message, a
  graceful argument-validation error (exit 1) where the issue reports
  a panic (exit 101), a compile error from a modified expression, or
  garbled output with the process still alive where the issue reports
  a crash. Artifacts that only show the tool runs (a version banner, a
  session list) show nothing about the bug.

## Honesty

- Where it lives: the report's result line and its prose claims, set
  next to what its artifacts actually show.
- What good looks like: the report claims exactly what its artifacts
  show. An honest cannot-reproduce is a pass: it says plainly it did
  not reproduce, shows the attempt's commands and output using the
  issue's trigger, and names what differed (OS, shell, version, input
  distribution). It fails when the words outrun the evidence: a root
  cause "verified" with no transcript, "guaranteed reproducible" with
  no artifact, "confirmed on two machines" with one shown, or a
  narration of a crash the output does not contain.

## Comms

- Where it lives: the claim comment read against the issue, and both
  comments read against the contribution policy in repo facts.
- What good looks like: the claim comment could only have been written
  about this issue. It names the behavior, the reproduction, or a
  concrete next step, and promises no fix, date, or guarantee. Fails:
  "kindly assign me, I will fix it within 2 days guaranteed", flattery
  plus a request to reserve the issue, or a bare "+1 same here".
- AI disclosure: read the policy's exact words. Only a policy that
  requires disclosing AI use ("all AI usage must be disclosed, stating
  the tool and extent") creates a disclosure requirement. There, a pass
  means a comment names the assistance. A policy that asks for comments
  to be human-written in the author's own voice, or that allows AI when
  the contributor takes responsibility, requires no disclosure. A
  human-voiced comment with no AI mention passes under it.
