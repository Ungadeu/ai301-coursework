# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. In live mode, read `scope.md` first to verify the target issue URL belongs to `codepath/pathreview-ai301-fa26-s1` and note any house rules. (In eval mode, skip `scope.md` and use only the package file.)
2. Read `rubric.md` to load all required and preferred checks along with the verdict rule, and read `references/evidence-guide.md` and `voice-guide.md` to know where each signal lives.
3. Read the issue description and the full comment thread from top to bottom, paying special attention to maintainer instructions, API constraints, and any repo conventions/policies in the repo-facts block.
4. Read the reproduction evidence (`repro_evidence` / posted reproduction report) to establish what was actually observed, what commands were run, and what was ruled out.
5. Read the candidate `plan.md` (Diagnosis, Scope, Files, Approach, Test Plan, Risks) and the draft `plan_comment` (`comment.md`) in full.
<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

## Evidence gathering

1. From the issue and comment thread, extract the reported bug behavior and any maintainer constraints (e.g., "do not add CLI flags", "keep current API", or scope limits) and repo conventions (e.g., AI disclosure requirements in `CONTRIBUTING.md`).
2. From the reproduction evidence, quote the exact reproduction command, the observed buggy output, and any diagnostic findings (such as whether disabling a cache or changing a flag still triggered the bug).
3. From the candidate `plan.md`, quote the claimed root cause under Diagnosis, the in-scope and out-of-scope statements under Scope, the target files and code changes under Files/Approach, and the verification command + expected output under Test Plan.
4. From the draft `plan_comment`, extract what the author promises to change, how they explain the cause, how they plan to test it, and whether required disclosures are present.
<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

## Check execution

1. Evaluate every check in `rubric.md` one by one in table order using only the gathered evidence.
2. For `diagnosis-grounded`, compare the plan's stated root cause directly against the reproduction evidence. If the reproduction evidence already proved that mechanism is not the cause (or if the plan only patches a symptom), grade `fail`.
3. For `bounded-scope`, verify that the plan states both what it will change and what it will not touch, and check that it does not sneak in unrelated cleanup, renames, or config migrations. Note: if a plan intentionally scopes down to fix a subset of the issue and explicitly states what it is deferring, grade `pass`.
4. For `executable-by-a-stranger` and `test-decisive`, verify that a stranger can tell which files/functions to edit without guessing (unless the issue itself lacks filenames and the plan clearly specifies the sequence of actions to locate and change them) and that the test plan gives a concrete expected output after the fix, not just "see if it works."
5. For `comment-faithful`, compare the draft comment against `plan.md`, the maintainer comments in the thread, `voice-guide.md`, and repo policies (including AI disclosure rules).
6. Assign `pass`, `fail`, or `unclear` to each check, accompanied by a concise one-line quote or factual citation from the package that decided the grade.
<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

## Verdict assembly

1. Review the grades of all `required` checks from `rubric.md`.
2. Treat any `unclear` grade on a `required` check as `fail`.
3. If every `required` check is `pass`, set the final verdict to `accept` (`ready`).
4. If one or more `required` checks are `fail` (or `unclear`), set the final verdict to `reject` (`hold`).
5. Do not allow `preferred` checks to alter the final verdict.
6. Print a short human-readable summary listing each check's grade and evidence, followed immediately by the required fenced JSON block as the very last item in the output.
<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
