# Unit 2 — Claim and Reproduce

Path: `eval/issues/issue-04.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

### GitHub username

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]
Ungadeu

---

## Posted upstream

### Claim comment

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]
Hi, I'd like to take this as a first contribution. In Proof mode, I'll check which of the basic rules (remove identity, fuse spiders, remove self loops) show no preview, then look at how the rules that do have previews are set up, and report back what I find. I will set up the environment to run tests and investigate the bug.

### Reproduction comment

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]
<https://github.com/codepath/ai301-unit1-starter/blob/6600671a692fef78e15263875393422c0ab88221/eval/issues/issue-04.md>
What I found: A rule's preview comes from its "picture" key in zxlive/rewrite_data.py, and only 4 Basic rules have one. zxlive/tooltips/ already contains remove_id.gif, fuse_spiders.gif, change_color_x.gif, change_color_z.gif and decompose_hadamard.gif, but no rule references them. I haven't checked whether they're the intended previews or whether GIFs render in the tooltip. I found no picture files for self-loops, parallel edges or unfuse.

**Result:** Reproduced on current `main`. With "Show rewrite previews" turned on, 8 of the
12 Basic rules show no preview, including all three named in the issue (Remove identity,
Fuse spiders, Remove self-loops). The 4 rules that have a preview picture show it correctly.

### Environment

- macOS 26.6.2 (x86_64)
- Python 3.14.3
- zxlive `main` at `d2f302c` (2026-08-21), installed with `pip install -e .` (it reports
  1.1.0, which is newer than the v1.0.0 release)
- PySide6 6.11.2, pyzx 0.10.6

#### Steps

```text
git clone https://github.com/zxcalc/zxlive.git && cd zxlive
python3 -m venv .venv && .venv/bin/pip install -e .
QT_QPA_PLATFORM=offscreen .venv/bin/python check_previews.py
```

`check_previews.py` builds each Basic rule the same way the Proof mode rules panel does, then
reads the tooltip it shows on hover. A rule with a preview returns an embedded `<img>`.

```python
from PySide6.QtWidgets import QApplication
app = QApplication([])
from zxlive.rewrite_data import action_groups
from zxlive.rewrite_action import RewriteAction
from zxlive.settings import display_setting
print("previews-show setting:", display_setting.previews_show)
for name, d in action_groups["Basic rules"].items():
    a = RewriteAction.from_rewrite_data(d)
    tip = a.tooltip
    print(f"{'PREVIEW   ' if '<img' in tip else 'NO PREVIEW'}  {a.name}")
```

### Output

```text
previews-show setting: True
NO PREVIEW  Remove identity
NO PREVIEW  Fuse spiders
NO PREVIEW  Remove self-loops
NO PREVIEW  Remove parallel edges
NO PREVIEW  Unfuse spider
NO PREVIEW  Save changed positions
PREVIEW     Copy 0/pi spider through its neighbour
PREVIEW     Push Pauli
NO PREVIEW  Colour change
PREVIEW     Strong complementarity
PREVIEW     Strong complementarity in opposite direction
NO PREVIEW  Decompose Hadamard
```

**Expected:** hovering a basic rule shows a preview picture, as it does for Copy, Push Pauli
and Strong complementarity.

**Actual:** Remove identity, Fuse spiders, Remove self-loops, Remove parallel edges, Unfuse
spider, Colour change and Decompose Hadamard show only a text tooltip.

**What I found:** A rule's preview comes from its `"picture"` key in `zxlive/rewrite_data.py`,
and only 4 Basic rules have one. `zxlive/tooltips/` already contains `remove_id.gif`,
`fuse_spiders.gif`, `change_color_x.gif`, `change_color_z.gif` and `decompose_hadamard.gif`,
but no rule references them. I haven't checked whether they're the intended previews or
whether GIFs render in the tooltip. I found no picture files for self-loops, parallel edges
or unfuse.

---

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

### Run history

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. Full run, original rubric: `agreement: 14/20 scored items  (bar: 18/20: below the bar)`.
   Two earlier attempts produced no score: the harness refused the rubric
   (`has no filled-in checks`, because the Weight cells were wrapped in backticks), then
   crashed because the `claude` CLI was not on PATH.
2. Partial run, revised rubric, `--only` on the six disagreements plus four canaries:
   `agreement: 10/10 scored items` (partial, so no bar verdict).
3. Full run, revised rubric: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.
4. Full run saved as `eval-run.txt`: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

### Package analysis

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

`pkg-09` (`sharkdp/fd#2033`). Gold label: accept, "honest cannot-reproduce: real attempt at
the argument-size reordering with marker-order artifacts, names what differed (uniform name
lengths, 2 MiB ARG_MAX) and what a triggering setup likely needs".

My original rubric rejected it. Its Repro Proof check read: "The report shows the exact error
or buggy output, and it matches the behavior described in the original issue." The report
says "Result: I could NOT reproduce scenario 2", and its artifact is `ONE ONE ONE TWO TWO TWO`,
which is in-order output. The grader failed it: "Logged output shows in-order execution (ONE
ONE ONE TWO TWO TWO); student states 'I could NOT reproduce scenario 2' — no buggy/reordered
output matching the issue's described behavior is shown." The check had only one way to pass
(show the bug), so an honest failed attempt could never pass it.

My final rubric accepts it, matching gold. Behavior Match now has a second pass case, "(b)
Honest cannot-reproduce: the report says plainly that it did not reproduce, shows artifacts
from a real attempt using the issue's trigger, and names what differed from the issue's
conditions." The grader passed it on that case: "real attempt using the issue's own trigger
(argument-size limit via --exec-batch), output shown (ONE/ONE/ONE/TWO/TWO/TWO), and an
explicit named difference ("uniform name lengths" vs. a possibly-needed differing length
distribution)."

### Check rationale

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

> | **AI Disclosure** | The contribution policy in the repo-facts block, then the claim comment and repro report | Pass if the repo's policy does not explicitly require disclosing AI use in comments, or if it does and the comments disclose it (naming the tool or the extent of assistance). A policy that only asks for comments to be human-written, or that allows AI with the contributor's responsibility, is not a disclosure requirement. Fail only if the policy explicitly requires disclosure of AI use and neither comment discloses. | required |

The first version read: "If the repository policy requires it, the user explicitly states if
AI was used to help write the comments." That wrongly rejected `pkg-03` (ripgrep, gold accept).
ripgrep's policy says "comments to maintainers must be written by humans in their own words".
That is a rule about who writes the comment, not a disclosure requirement, but the grader
read it as one: "repo_policy requires comments 'be written by humans in their own words' ...
but neither the claim comment nor the repro report states anything about AI use." So the
check now names the one wording that triggers it ("explicitly require disclosing AI use") and
lists the two policy types that don't. I rejected dropping the check or making it
`preferred`: `pkg-20` (ghostty, "All AI usage in any form must be disclosed") is the only
`disclosure` package, and without a required check that sees it, the category floor fails.

### Trade-offs

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

Loosening AI Disclosure risked flipping the one package it exists to catch, so I added canaries
to the `--only` re-run: `pkg-20` (the only `disclosure` package) and `pkg-07` (p5.js, which
passes because its comment discloses AI assistance). Both held:

```text
pkg-07  accept  accept   yes
pkg-20  reject  reject   yes
```

The confirming full run then showed `disclosure 1/1`.

A case I accept it will miss: in a repo like ripgrep, whose policy asks for human-written
comments and says "AI-generated comments may be hidden", a comment that is plainly
AI-generated now passes this check, because the check only asks for disclosure and no other
check reads whether a comment is human-voiced. I accepted that because the eval has no such
package, and tone and voice belong in my voice guide, which live mode applies and eval mode
ignores.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
