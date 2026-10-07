# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->
- **Be polite, concise, and objective:** Communicate like a collaborative engineer on a shared open-source thread.
- **Promise only what is in the plan:** State clearly what root cause you traced, what bounded change you plan to make, and how you will test it. Do not promise timelines/dates or extra features not in `plan.md`.
- **Engage maintainer context:** If a maintainer left guidance in the thread (such as keeping the existing API), explicitly align your proposed approach with their guidance.
- **Follow repo disclosure conventions:** If the repository's policy requires disclosing AI tool usage, include a clear, honest disclosure line in the comment.
- **Use clean formatting:** Use short paragraphs, bullet points, and inline code backticks (`filename.py`, `function_name()`) so maintainers can scan your plan in seconds.

## Who I am in threads

I am a Master's student and aspiring AI engineer contributing to open-source to build my software development experience. I aim to be a collaborative and transparent contributor, communicating objectively and ensuring my work respects repository standards and maintainer guidance. Readers can expect me to provide clear evidence for my findings and focus on bounded, well-tested fixes.
<!-- Paste your week-2 section here. -->

## Rules I write by

### Rule: Stick to the Plan (and No Timelines)

I clearly state the traced root cause, the bounded change, and the test plan, without promising exact delivery dates or extra features outside the scope.

- Wrong: "I will fix this bug and also clean up the other functions in the file by tomorrow afternoon."
- Right: "I plan to update `clean_text()` to handle the unhandled edge case. I will not modify the surrounding helper functions."

### Rule: Respect Maintainer Guidance

If a maintainer leaves instructions or constraints (like preserving an API or avoiding a specific module), I explicitly acknowledge and align my approach with their guidance.

- Wrong: "I decided to rewrite the API to make it more efficient."
- Right: "Per your note about keeping the existing API, my plan only modifies the internal validation logic and leaves the function signature unchanged."

### Rule: Transparent AI Disclosure

I always include a clear, honest disclosure line in my comments if the repository policy requires stating AI tool usage.

- Wrong: "I figured out this fix on my own."
- Right: "*(Note: Prepared with AI assistance via Claude Code.)*"
<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->

## Things I never post

- Exact delivery dates, timelines, or guarantees (e.g., "I'll have the PR up in 2 hours").
- Promises to fix unrelated issues or perform "while I'm at it" refactoring.
- Guesses or assumptions about a bug's root cause without direct reproduction evidence to back it up.
- Piggybacked reproductions (e.g., "Same as above, can confirm") without showing my own terminal output.
- Comments that hide or obscure the use of AI coding assistants when repository policies require disclosure.
<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->
