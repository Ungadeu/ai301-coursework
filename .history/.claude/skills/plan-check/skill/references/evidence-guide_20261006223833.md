# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->
## 1. Issue & Maintainer Thread (`issue`, `comment_thread`)

- **Where it lives (Eval mode):** Under the `## Issue` and `## Comment thread` (or `### Comments`) headings in the package markdown file.
- **Where it lives (Live mode):** The GitHub issue body and comments fetched from `https://github.com/codepath/pathreview-ai301-fa26-s1/issues/<N>`.
- **What to look for & what good looks like:** Look for the original bug symptom and any maintainer guidance (e.g., "keep the current API", "do not touch module X", or hints about where the bug is). Good plan comments acknowledge and obey these maintainer signals rather than ignoring them.

## 2. Repo Facts & Conventions (`repo_facts`)

- **Where it lives (Eval mode):** Under the `## Repo facts` (or `## Repository context`) block in the package markdown file.
- **Where it lives (Live mode):** The repository's `README.md`, `CONTRIBUTING.md`, `CLAUDE.md`, and directory tree in the Path Review repo.
- **What to look for & what good looks like:** Look for actual file paths in the repo, test runner commands (`pytest`, etc.), and contribution policies—especially AI disclosure rules (e.g., if the repo requires disclosing AI assistance in comments/PRs) or formatting conventions. Good plans reference real files that exist in the repo, and good comments include required disclosures when repo policy mandates them.

## 3. Reproduction Evidence (`repro_evidence`)

- **Where it lives (Eval mode):** Under the `## Repro evidence` (or `## Reproduction` / author's prior repro comment) section in the package file.
- **Where it lives (Live mode):** Quoted directly inside the student's `plan.md` and/or their posted Unit 2 reproduction comment on the GitHub issue thread.
- **What to look for & what good looks like:** Look for the exact command run, the environment, the actual buggy output observed, and any experiments run during reproduction (for example, "ran with `--no-cache` and the bug still occurred"). A good diagnosis in `plan.md` must be consistent with this evidence; if the repro proved the cache wasn't involved, a plan that blames the cache fails `diagnosis-grounded`.

## 4. Candidate Plan (`plan`)

- **Where it lives (Eval mode):** Under the `## Plan` (or `## plan.md`) section of the package file.
- **Where it lives (Live mode):** The local `plan.md` file specified in the command.
- **What to look for & what good looks like:**
  - **Diagnosis:** Traces upstream from the symptom in `repro_evidence` to the true root cause in code.
  - **Scope:** Explicitly lists both `In scope:` and `Out of scope:` (or `Not in scope:`). Keeps changes minimal and bounded (no "while I'm here" refactoring, renaming helpers, or unrelated docs passes). Intentionally scoping down to part of an issue is valid if explicitly stated.
  - **Files & Approach:** Names the specific source and test files to touch and explains the exact logic change clearly enough that another engineer could implement it without guessing.
  - **Test Plan:** Re-runs the exact repro command/input from `repro_evidence` and states the concrete expected output after the fix (e.g., "Today: 4 pages. Expected after fix: 3 pages"), plus any unit tests to add/run.

## 5. Draft Plan Comment (`plan_comment`)

- **Where it lives (Eval mode):** Under the `## Plan comment` (or `## Draft comment` / `## comment.md`) section of the package file.
- **Where it lives (Live mode):** The local `comment.md` file specified in the command.
- **What to look for & what good looks like:** A concise, polite public comment for the issue thread that states: (1) what root cause was found based on the reproduction, (2) what bounded change is proposed, and (3) how it will be verified. It must match `plan.md` (never promising extra features or different files), follow `voice-guide.md`, and satisfy any repo disclosure conventions.

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->
