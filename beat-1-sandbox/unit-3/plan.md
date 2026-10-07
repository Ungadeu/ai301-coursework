# Implementation Plan — Issue #555 (zxcalc/zxlive, eval issue-04)

Issue: "Missing several basic rule previews" — "Including remove identity, fuse
spiders, remove self loops, etc." (opened by RazinShaikh, COLLABORATOR, 2026-08-04;
labels: Type: bug, good first issue, Category: Proof mode).

## 1. Diagnosis

From my Unit 2 reproduction on `main` at `d2f302c` (macOS 26.6.2, Python 3.14.3,
PySide6 6.11.2, pyzx 0.10.6):

```bash
QT_QPA_PLATFORM=offscreen .venv/bin/python check_previews.py
```

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

Cause: `RewriteAction.from_rewrite_data()` in `zxlive/rewrite_action.py` only sets
`picture_path` when the rule's data has a `"picture"` key (a file in
`zxlive/tooltips/`) or `"custom_rule"`. The 8 entries above in the `rules_basic` dict
in `zxlive/rewrite_data.py` have neither, so `picture_path` is `None` and the
`tooltip` property returns plain text.

Correction to my Unit 2 report: I said the GIFs in `zxlive/tooltips/`
(`remove_id.gif`, `fuse_spiders.gif`, ...) might be the missing previews. I checked,
and they are not. They were added in "add gif clips for demo of basic/graph/zxw/zh
rewrites". Each is a 38–45 frame screen recording of the app, and `QPixmap.load()`
reads only frame 0, which shows the old rules sidebar and the graph *before* the
rewrite. The real previews are static before/after PNGs, added later in "Add preview
pictures to rewrites (#309)". No PNG exists for any of the 8 rules above.

The `tooltip` property already has a second path that needs no image file: when
`picture_path == 'custom'` it renders `self.lhs_graph` and `self.rhs_graph` side by side
with an `=` between them. Custom rules use it today. Basic rules can use the same path
if they carry a small example `lhs`/`rhs` graph. I prototyped this in a scratch clone:
the 6 pyzx-backed rules apply cleanly to small examples, each resulting `rhs` is
tensor-equal to its `lhs` (`pyzx.compare_tensors(..., preserve_scalar=False)` →
`True`), and the rendered tooltips show the expected before/after pictures.

## 2. Scope

- **In scope:** generated previews for 7 Basic rules: Remove identity (`id_simp`),
  Fuse spiders (`fuse_simp`), Remove self-loops (`remove_self_loops`), Remove parallel
  edges (`hopf`), Colour change (`cc`), Decompose Hadamard (`euler`) and Unfuse spider
  (`unfuse`). Also a one-branch change in `from_rewrite_data()` so data with
  `lhs`/`rhs` but no `"picture"` uses the existing render path, plus tests.
- **Not in scope (boundary):**
  - "Save changed positions" (`ocm`). It only saves vertex positions and is not a
    graph rewrite, so there is nothing to show before/after. It stays text-only.
  - The look of the existing `'custom'` renderer (the `=` sign sits below centre, and
    each side is scaled to fit separately). Custom rules share it, so changing it
    belongs in its own change.
  - New image files, the existing PNG/GIF assets, and rules in other groups
    (Graph-like, ZXW, ZH, fault-equivalent).
  - Setting `"custom_rule": True` on basic rules. That flag also sets
    `is_custom_rule`, which `rewrite_action.py` uses elsewhere, so I won't use it.

## 3. Files to Touch

- `zxlive/rule_previews.py` (new): small example graphs and a function that attaches
  `lhs`/`rhs` to the Basic rules.
- `zxlive/rewrite_data.py`: call that function once, right after `rules_basic` is
  defined.
- `zxlive/rewrite_action.py`: in `from_rewrite_data()`, add
  `elif 'lhs' in d and 'rhs' in d: picture_path = 'custom'` after the `'picture'`
  branch.
- `test/test_rule_previews.py` (new): regression tests.

## 4. Approach

1. In `zxlive/rule_previews.py`:
   - A helper `_chain(types, edges, phases)` that builds a one-row graph with
     `new_graph()` from `zxlive.common`. Vertices go at `qubit=0`, `row=0,1,2,...`, so
     they lay out left to right.
   - One example `lhs` and the match vertices for each pyzx-backed rule:
     - `id_simp`: boundary – Z – boundary; match the Z.
     - `fuse_simp`: boundary – Z(π/2) – Z(π/4) – boundary; match the two Z spiders.
     - `remove_self_loops`: boundary – Z (with a self-loop) – boundary.
     - `hopf`: boundary – Z =(two parallel edges)= X – boundary.
     - `cc`: boundary – Z(π/2) – boundary.
     - `euler`: boundary – Z –(Hadamard edge)– Z – boundary.
   - `add_basic_rule_previews(rules)`: for each of those keys, deep-copy `lhs` and call
     `rules[key]["rule"].apply(rhs, *match)`, so every `rhs` is produced by the real
     rule rather than drawn by hand. Then set `rules[key]["lhs"]` and
     `rules[key]["rhs"]`.
   - For `unfuse`, `UnfusionRewrite.apply()` deliberately raises
     `NotImplementedError` because it is interactive. Unfusing is fusing in reverse,
     so its preview is the `fuse_simp` example swapped (`lhs` = fused spider,
     `rhs` = the two spiders).
2. In `zxlive/rewrite_data.py`, call `add_basic_rule_previews(rules_basic)` after the
   dict. The graphs are a few vertices each. Rendering stays lazy (it only happens the
   first time a tooltip is read), so startup cost is negligible.
3. In `zxlive/rewrite_action.py`, add the one `elif` branch from section 3. Rules that
   have a `"picture"` keep using it, because that branch is checked first.
4. In `test/test_rule_previews.py`:
   - `test_basic_rules_have_previews`: parametrized over the 7 keys. It builds each
     `RewriteAction` via `from_rewrite_data()` with `display_setting.previews_show`
     on, and asserts that `"<img"` is in the `tooltip`.
   - `test_preview_rhs_matches_lhs`: for each of the 6 rule-derived examples, asserts
     `pyzx.compare_tensors(lhs, rhs, preserve_scalar=False)` after `auto_detect_io()`.
   - `test_ocm_has_no_preview`: asserts "Save changed positions" still has no
     `"<img"` in its tooltip, so the boundary in section 2 is tested.
   - `test_preview_rules_are_not_custom`: asserts these actions have
     `is_custom_rule is False`.

## 5. Test Plan

1. Re-run my Unit 2 reproduction exactly:
   `QT_QPA_PLATFORM=offscreen .venv/bin/python check_previews.py`
   - Before: 8 `NO PREVIEW` lines (listed in section 1).
   - After: `PREVIEW` for Remove identity, Fuse spiders, Remove self-loops, Remove
     parallel edges, Unfuse spider, Colour change and Decompose Hadamard. The 4 that
     already had a preview stay `PREVIEW`, and only `NO PREVIEW  Save changed positions`
     remains, so 11 of 12 show a preview.
2. `pytest test/test_rule_previews.py -v`: all tests pass (7 + 6 parametrized cases,
   plus the 2 single tests).
3. The repo's CI checks: `pytest test/`, `mypy zxlive`, `ruff check`, and
   `complexipy . --max-complexity-allowed 15`. All pass, so the new branch in
   `from_rewrite_data()` must not push it over the complexity limit.
4. Manual: launch `python -m zxlive`, open Proof mode, and hover over each of the 7
   rules to confirm the before/after picture shows.

## 6. Risks / Unknowns

- **Style.** Generated previews look like the app's own graph rendering, not like the
  hand-drawn PNGs (no `α`-style generic phases, and no "…" for arbitrary arity). The
  maintainers may prefer artwork. I'm asking on the issue before building.
- **The renderer looks a bit off.** In the prototype the `=` sits below centre and
  boundary dots are clipped at the picture edge. That comes from the existing
  `'custom'` renderer, which is out of scope here.
- **The previews depend on pyzx.** If pyzx changes how a rule rewrites (for example
  where `euler` places new vertices), the generated picture changes with it. The
  tensor-equality test catches a wrong picture but not an ugly one.
- **Unfuse isn't produced by its own rule.** Its preview is the fuse example
  reversed. This is correct for the default unfusion, but it doesn't show the
  dialog's other options.

## Deviations

The build changed only the four planned files (`zxlive/rule_previews.py`,
`zxlive/rewrite_data.py`, `zxlive/rewrite_action.py`, `test/test_rule_previews.py`)
on branch `fix/555-generated-rule-previews` in `Ungadeu/zxlive`. The approach held.
Four things differed from the plan:

1. **Base commit.** I planned against `d2f302c` but built on the current `master`,
   `7cb6b71` (15 commits newer). Before branching I checked that `from_rewrite_data()`,
   the `tooltip` property and `rules_basic` are unchanged on `master`, and re-ran the
   reproduction there. It gave the same 8 `NO PREVIEW` lines, so the diagnosis still
   applies. Upstream PR #574 ("Add tooltip diagram preview to patterns sidebar",
   merged 2026-08-11) touched tooltip rendering, but for the editor's patterns
   sidebar, not proof-mode rules, so it doesn't overlap with this issue.
2. **How the rule is applied.** The plan said to call `rules[key]["rule"].apply(rhs,
   *match)`. mypy rejects that because the base `Rewrite` type has no `apply`. Like the
   existing code in `RewriteAction.do_rewrite()`, I cast to `RewriteSingleVertex` or
   `RewriteDoubleVertex` depending on how many vertices the example matches. The
   behavior is the same.
3. **Running the tests locally needed a temporary workaround.** On macOS,
   `test/conftest.py` raises `RuntimeError: Unable to derive QSettings base path` before
   any test runs, on `master` as well. That's because Qt names the native settings file
   `com.<org>.<app>.plist`, a layout the probe doesn't accept. CI runs on Linux, so it
   isn't affected. To run the suite I patched `conftest.py` locally, ran everything,
   then restored it with `git checkout -- test/conftest.py`, so the workaround is not on
   the branch. It's a separate bug and out of scope for this issue.
4. **Manual GUI check not done yet.** Test Plan step 4 (hovering each rule in the
   running app) is still to do by hand. The automated checks below cover the same
   tooltips offscreen.

Test plan results:

- Reproduction before (`7cb6b71`): 8 `NO PREVIEW`. After: `PREVIEW` for Remove
  identity, Fuse spiders, Remove self-loops, Remove parallel edges, Unfuse spider,
  Colour change and Decompose Hadamard. Only `NO PREVIEW  Save changed positions`
  remains (11 of 12), as planned.
- `pytest test/test_rule_previews.py -v`: 15 passed (7 + 6 parametrized, plus 2).
- `pytest test/`: 214 passed. `mypy zxlive`: no issues in 34 files. `ruff check` and
  `ruff check . --select=PLR0912`: all checks passed. `complexipy . --max-complexity-allowed 15`:
  all functions within the limit.
