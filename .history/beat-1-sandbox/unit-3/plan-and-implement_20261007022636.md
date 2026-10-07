# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]
Ungadeu
**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]
<https://github.com/Ungadeu/ai301-unit1-starter-issue4/blob/b993e3cb5bda9d6788cf50a3f15a834a7972d393/eval/issues/issue-04.md>
---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]
eval/issues/issue-04.md
**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]
Scoreboard:

Agreement: 19/20, which clears the 18/20 bar.
Categories: each one has at least one match: clear-accept 6/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4.
The one miss: pkg-14 is labelled accept, but your skill rejected it because it failed executable-by-a-stranger.
**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]
pkg-03  clear-accept  accept  accept   yes
**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]
| **comment-faithful** | `plan_comment`, `plan`, `comment_thread`, `repo_facts` | The draft `plan_comment` summarizes the diagnosis, approach, and verification plan faithfully without promising changes outside `plan`, directly respects any maintainer constraints or direction in `comment_thread`, and follows all repository policies in `repo_facts` (such as required AI-assistance disclosure or branch/API rules). | required |
**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]
Requiring diagnosis-grounded to verify that the root cause is directly supported by repro_evidence means that if an issue has a sparse reproduction report where the root cause can only be inferred by reading source files not quoted in the reproduction, my rubric will grade the check unclear (and therefore reject). I verified this behavior by checking my results across the wrong-cause and clear-accepts categories in eval-run.txt, confirming that tightening this check caught the wrong-cause packages without falsely rejecting valid scoped plans..
---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
