# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| **Claim Intent** | The claim comment, read against the issue's title and body | Pass if the comment is specific to this issue (it names the issue's behavior, the reproduction, or a concrete next step) and promises no fix, deadline, or guarantee. Fail if it is interchangeable boilerplate that could be pasted on any issue, asks only to be assigned or to reserve the issue, promises a fix or a timeline ("fix within 2 days"), or states no intent at all (a bare +1). A softly worded intent ("I'd like to look into this") passes. | required |
| **Environment Record** | The repro report's environment record, read against the versions and platform the issue targets (issue body, thread highlights, and the bug-report template in the repo-facts block) | Pass if the report names the OS and the version of the tool under test, plus any runtime, driver, or platform detail the issue says the bug depends on, AND those versions match what the issue targets or the report explicitly names the difference. Which runtime counts depends on the project's language; a Rust or Go CLI needs no Python/Node version. Fail if there is no environment record, or if the report tested a different version or platform than the issue targets without acknowledging it. | required |
| **Followable Steps** | The repro report's steps, read against the trigger the issue describes | Pass if a stranger with only public resources could re-run the steps from a starting state to the trigger: every command, input file, and config needed is shown or is publicly available. Fail if the reproduction depends on private or unshared code, config, or data, or if the steps omit a condition the issue says is required to trigger the bug (a flag, a driver, a platform). | required |
| **Behavior Match** | The repro report's artifacts (output excerpts, logs, tracebacks, prompt captures) read against the behavior the issue describes, plus the report's stated result | Pass in either of two cases. (a) Reproduced: an artifact produced by the issue's own trigger shows the issue's behavior (same error, exit status, or wrong output), not an adjacent symptom. (b) Honest cannot-reproduce: the report says plainly that it did not reproduce, shows artifacts from a real attempt using the issue's trigger, and names what differed from the issue's conditions. Fail if there is no artifact at all, if the artifact shows a different behavior than the issue's (a different error, a graceful validation message where the issue reports a crash, a still-running process where the issue reports a crash) but the report narrates it as confirmation, or if the report claims more than its artifacts show (a root cause, "guaranteed reproducible", results on machines it does not show). | required |
| **AI Disclosure** | The contribution policy in the repo-facts block, then the claim comment and repro report | Pass if the repo's policy does not explicitly require disclosing AI use in comments, or if it does and the comments disclose it (naming the tool or the extent of assistance). A policy that only asks for comments to be human-written, or that allows AI with the contributor's responsibility, is not a disclosure requirement. Fail only if the policy explicitly requires disclosure of AI use and neither comment discloses. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept (ready to post) only if every required check passes. Reject (hold) if any required check fails. Treat `unclear` as a fail, so an unclear required check also means reject. Preferred checks, if any are added, never change the verdict. An honest cannot-reproduce that passes Behavior Match case (b) is an accept, not a reject.
