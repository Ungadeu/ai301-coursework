# Playbook: Uriel Ngadeu

## Response rules

- Open every reply by answering the reviewer's actual technical point in the first sentence—state what I changed (with file/function names in backticks) or give concrete test/code evidence if I need to clarify a choice.
- Thank the reviewer once and precisely for the specific catch or guidance; never write defensive explanations, apologies about being busy, or excuses about tooling.
- Address every comment from a review round in one single reply after pushing batched commits, and never claim work or test runs I have not actually verified locally.

## Staleness thresholds

- EdgeTX has no root `CONTRIBUTING.md` specifying a review SLA. Checking five recent merged PRs from outside contributors on `EdgeTX/edgetx` (PRs `#8094`, `#8088`, `#8082`, `#8078`, `#8076`, checked 2026-11-23), the first maintainer response (a comment, or the merge itself when there was none) took from under 1 hour to about 2 days (median ~0.4 days, about 10 hours). All five were merged by @pfeerick within 2 days of opening.
- Wait at least **7 quiet days** (days since anyone other than me or a bot commented) before sending a first-review nudge. That is more than 3× the slowest response I measured, which leaves room for weekends and volunteer maintainers.
- After an active review round where I have replied and pushed updates, wait at least **7 quiet days** before sending one follow-up nudge.
- Bot comments (`github-actions`, the MemBrowse memory report) are not maintainer activity: they don't reset the quiet-day count and don't count as review feedback.

## Nudge etiquette

- Send at most one polite nudge per waiting period, only after the staleness threshold above is met; never send a second unanswered nudge.
- Make the nudge self-contained in 2–3 sentences: one sentence summarizing what the PR does, one clear ask (review or answer to one specific question), and zero urgency or deadline pressure.
- Tag at most the reviewer who already engaged in the thread (or tag nobody on a brand-new PR with no reviewer yet); never @-pile maintainers.

## Walk-away criteria

- Close my own PR if a maintainer says the approach does not fit EdgeTX's direction, if another PR resolves `#1067` first, or if the PR stays completely quiet for **30 days** past my single nudge.
- Keep the closing note to 2–3 polite sentences stating the reason clearly (e.g., superseded or closed to keep the queue clean) and thanking the maintainers for their time.
