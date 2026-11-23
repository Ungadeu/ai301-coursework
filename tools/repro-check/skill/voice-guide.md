# Voice guide: how I talk upstream

## Who I am in threads

I am a Master's student and aspiring AI engineer contributing to open-source to build my software development experience. I aim to be a collaborative and transparent contributor, communicating objectively and ensuring my work respects repository standards and maintainer guidance. Readers can expect me to provide clear evidence for my findings and focus on bounded, well-tested fixes.

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

### Rule: Objective and Concise Formatting
I communicate objectively using short paragraphs, bullet points, and inline backticks so my plan is easy for maintainers to scan in seconds.
- Wrong: "I was looking at the file and it seems like the function is acting weird so I will try to fix the variable."
- Right: "The bug originates in `prompt_defense.py` where `sanitize_input()` fails to catch newline characters."

## Things I never post

- Exact delivery dates, timelines, or guarantees (e.g., "I'll have the PR up in 2 hours").
- Promises to fix unrelated issues or perform "while I'm at it" refactoring.
- Guesses or assumptions about a bug's root cause without direct reproduction evidence to back it up.
- Piggybacked reproductions (e.g., "Same as above, can confirm") without showing my own terminal output.
- Comments that hide or obscure the use of AI coding assistants when repository policies require disclosure.