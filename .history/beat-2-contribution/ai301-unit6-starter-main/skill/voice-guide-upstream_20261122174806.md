# Voice guide, the upstream section: how I talk to maintainers

## Upstream: how I talk to maintainers

### Claims I post

#### Rule: Promise only what is in the plan

State clearly what root cause you traced, what bounded change you plan to make, and how you will test it. Do not promise timelines/dates or extra features not in `plan.md`.

#### Rule: Engage maintainer context

If a maintainer left guidance in the thread (such as keeping the existing API), explicitly align your proposed approach with their guidance.

### Questions I ask

#### Rule: Show what I tried and ask one clear question

Before asking a maintainer anything, I state what I already checked or ran (with relevant file names or function names in backticks) and ask one specific question they can answer quickly from their chair, instead of dumping a list of five questions at once.

- Wrong: "I'm stuck on this issue. How does the parser work, which file should I edit, and how do I run the tests?"
- Right: "I traced the parsing error to `parse_config()` in `config.py` and verified it fails under `pytest tests/test_config.py`. Should empty keys raise a `ValueError` here, or fall back to the default dict?"

#### Rule: Keep questions scannable and grounded in repo context

I keep questions short, objective, and aligned with existing docs or prior maintainer comments so the maintainer does not have to repeat guidance that is already in the thread.

- Wrong: "I read through a bunch of files and wasn't totally sure what you meant earlier about keeping backwards compatibility, could you explain the whole design?"
- Right: "Per your note on preserving backwards compatibility for `load_items()`, would adding an optional `strict=False` parameter fit the API, or would you prefer an internal-only fix?"

### Pings I send

#### Rule: Match the repo's reply rhythm with zero pressure

I only follow up after waiting longer than the repository's normal response pace—never based on my own deadline—and I keep the note brief, polite, and free of guilt or urgency.

- Wrong: "Hi, just bumping this! I need this reviewed by Friday for my schedule—any chance you can look at it today?"
- Right: "Hi—checking in on this when you have a moment. No rush at all; please let me know if any part of the approach or tests needs adjustment."
