# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

### Issue link

[https://github.com/codepath/pathreview-ai301-fa26-s1/issues/11](https://github.com/codepath/pathreview-ai301-fa26-s1/issues/11)

### Verdict output


{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/11",
  "checks": [
    {"name": "Maintainer Alive", "grade": "pass", "evidence": "Latest default-branch commit 2026-09-16 by human Aburke225, 27 days before today (within 90)"},
    {"name": "Repo in Use", "grade": "pass", "evidence": "archived: false; last push 2026-09-16, within 90 days (no releases)"},
    {"name": "Newcomer Scope", "grade": "pass", "evidence": "Single bounded docs task in docs/ARCHITECTURE.md, est. 2-3 hours; labels good first issue/docs/rag/tier-1; 0 comments; opener is COLLABORATOR"},
    {"name": "Unclaimed Status", "grade": "pass", "evidence": "No assignees, no comments, no open or closed PR references #11"},
    {"name": "Contribution Policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and PR template contain no statement on AI-assisted contributions (silence passes)"},
    {"name": "Technical Fit", "grade": "pass", "evidence": "Documents hybrid vector+keyword retrieval scoring, matching RAG/ChromaDB experience; no front-end work"}
  ],
  "verdict": "accept"
}
---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

One complete run is on record, and it is the run committed as `eval-run.txt`:

1. `agreement: 20/20 scored items  (bar: 18/20: PASS)`

Category breakdown on that run, from the same file:

```text
categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4
agreement: 20/20 scored items  (bar: 18/20: PASS)
```

That run is the one written by the harness itself, and its provenance header ties it to
the rubric in this repository:

```
# eval run written by run_eval.py at 2026-09-22T17:09:13Z
# model: sonnet (pinned)
# packages: 20 scored
#   rubric.md  sha256:97a37edafea08cfa
```

The sha256 of the current `tools/.claude/skills/issue-select/skill/rubric.md` is
`97a37edafea08cfa`, matching that header, so the committed run was produced by the
rubric as it now stands. The run was independently reproduced in full on the same
rubric, returning the same 20/20 and the same per-category breakdown.

**Issue analysis**

`issue-11` — my rubric returned **accept**; the gold label is **accept**. They agree.

The gold entry records the issue as `zxcalc/zxlive#555`, category `clear-accept`, with
the note:

> "small active repo, maintainer-filed bounded bug, unclaimed"

My rubric reached accept because all five `required` checks passed:

- **Maintainer Alive** — "The newest commit is from 2026-09-16 by Aburke225, a person, not a bot. That is 27 days ago, inside the 90-day window."
- **Repo in Use** — "The repo is not archived and was last pushed on 2026-09-16, within 90 days. It has no releases, which is fine because the push date alone satisfies the check."
- **Newcomer Scope** — "It asks for one bounded thing: a new section in docs/ARCHITECTURE.md, estimated at 2–3 hours. It has 4 labels, including good first issue, has 0 comments, and was opened by a collaborator. It is not an umbrella issue."
- **Unclaimed Status** — "No one is assigned, there are no comments, and no open or closed PR mentions #11. Two PRs matched my keyword search by accident (#111 and #89), and neither is about this issue."
- **Contribution Policy** — "docs/CONTRIBUTING.md and the PR template say nothing about AI-assisted work, and your rubric counts silence as a pass."
- **Technical Fit**: "It's a docs task about hybrid retrieval scoring in the RAG pipeline. That matches your RAG and ChromaDB experience and your preference for backend work over front-end." 

**Check rationale**

Quoted from `tools/.claude/skills/issue-select/skill/rubric.md` as it is currently
written:

> | Maintainer Alive | repo-facts block: the "last 5 default-branch commits" list (dates
> and author names), and the "maintainer first-response sample" | At least one of the 5
> most recent default-branch commits is dated within 90 days of the capture date and
> reflects human activity. A commit authored by a bot (username ending in `[bot]`, or a
> `*-bot` service account) counts as human activity when its message shows it merged a
> person's pull request (e.g. "Merge pull request #123 from alice/fix-docs"); a bot's own
> routine upkeep, such as a version bump or a leaderboard refresh, does not. Judge the
> repo, not this issue: an issue with no maintainer reply still passes when the commit
> list is live. Use the first-response sample only to break a tie when commit recency is
> borderline. | required |

The check began as a much narrower rule. In its earlier form (commit `16a7406`) it read:

> | Maintainer Alive | comment thread, issue body | A maintainer has commented on,
> labelled, or authored the issue within the last 30 days. | required |

Three things changed, each for a reason:

1. **Evidence moved from the issue thread to the repo's commit list.** The old wording
   measured whether a maintainer had engaged with *this issue*, which is a property of
   the issue's popularity, not of whether the project is alive. A perfectly good,
   quietly-filed issue in a busy repo has no maintainer reply at all. The explicit
   sentence "Judge the repo, not this issue" was added to settle that.
2. **The window widened from 30 to 90 days.** Thirty days is inside the normal quiet
   period of a small but healthy project, so it produced false rejections rather than
   catching dead repos.
3. **Bot commits are handled explicitly.** A repo whose only recent commits are a bot's
   version bumps is not alive, but a bot commit that merges a person's pull request is
   evidence of a human maintainer acting. Without that distinction the check reads
   automated upkeep as a pulse.

**Trade-offs**

### A canary re-run with `--only`

I extracted the earlier version of the rubric from
commit `16a7406` and re-ran three `clear-accept` issues against it:

```text
python3 run_eval.py --rubric rubric-old.md --only issue-09,issue-14,issue-01

item      gold    verdict  agree  note
issue-01  accept  reject   NO     failed: Maintainer Alive, Newcomer Scope, Technical Fit (preferred)
issue-09  accept  reject   NO     failed: Maintainer Alive, Technical Fit (preferred)
issue-14  accept  reject   NO     failed: Maintainer Alive, Technical Fit (preferred)

agreement: 0/3 scored items
```

All three were false rejections, and `Maintainer Alive` was the required check that sank
every one of them. Since `clear-accept` is 8 of the 20 scored items, the old thread-based
wording was the single largest source of error in the rubric, and rewriting it is what
moved that category to 8/8.

### What the current wording gives up

By judging the repo's commit list rather than
maintainer responsiveness, the check can no longer detect a repo that ships code steadily
but never answers contributors. The `first-response sample` is demoted to a tiebreaker
"only ... when commit recency is borderline," so it does not fire when commits are clearly
recent. `issue-12` is exactly that shape and shows the cost concretely — under the current
rubric it passes Maintainer Alive:

> "Most recent default-branch commit is dated 2026-08-12, same day as capture, and
> reflects a merged human PR (#4080)."

while its own repo-facts block records no maintainer reply on either sampled issue:

> "#4095 (opened 2026-08-12): no maintainer comment in thread"
> "#4093 (opened 2026-08-10 by a maintainer): no maintainer comment in thread"

`issue-12` still rejects, but only because `Contribution Policy` fails on
"We do not accept AI-generated code or documentation." That makes Contribution Policy the
sole load-bearing check on the only `policy` item in the set: remove it and `issue-12`
becomes an accept, dropping agreement to 19/20 *and* leaving `policy` at 0/1, which fails
the category floor even though 19 still clears the 18/20 threshold. I accept that
Maintainer Alive will miss the unresponsive-but-committing repo, because catching it with
a stricter thread rule costs three `clear-accept` issues for every one it saves.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

Fit to my interests and time available: Issue #11 asks for a bounded documentation
section in docs/ARCHITECTURE.md explaining hybrid vector-and-keyword retrieval
scoring in the RAG pipeline, estimated at 2–3 hours. That directly matches my fit
profile in scope.md—I have hands-on experience with Python, RAG pipelines, and
ChromaDB, prefer backend/data topics over front-end UI work, and want more practice
with collaborative Git workflows on a clear, scoped first contribution.

What the verdict identified correctly vs. what I weighed manually: The rubric
correctly verified that the repo is actively maintained (recent human commit by
Aburke225), unclaimed (no assignees, comments, or linked PRs), bounded to a single
file, and aligned with my RAG background. What the rubric could not weigh is how much
code reading across the retrieval modules will be required to make sure the
architecture explanation accurately reflects the current implementation rather than
high-level guesses, as well as the fact that a pure documentation task gives me less
hands-on unit-testing practice than a code bug would.

Anticipated difficulty in claiming it: Low. The issue has zero comments, no
assignees, and no open PRs referencing it, so claiming it cleanly should be
straightforward as long as I verify the retrieval source code first so my claim
comment shows I understand the relevant files before starting.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
