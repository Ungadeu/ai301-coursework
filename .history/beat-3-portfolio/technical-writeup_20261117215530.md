# Securing Prompt Defenses and Automating PR Inspections

## Overview

For my final project, I tackled a newline prompt injection vulnerability (Issue #64) in an open-source repository while simultaneously building an automated pull request grading tool (`pr-precheck`). The problem was two-fold: the codebase was vulnerable to malicious newline inputs, and manually reviewing PRs for scope drift and debris was time-consuming. I successfully wrote a Python fix and Pytest coverage for the vulnerability, and built a Claude-powered tool to strictly enforce repository guidelines. Today, the PR is submitted, and my local tool actively guards against undocumented changes.

## What happened

My journey began with fixing the prompt injection bug in `safety/prompt_defense.py`. I reproduced the vulnerability and mapped out a plan, but my first attempt at building the code fell short when I ran the repository's strict pre-commit hooks. The tests failed due to unused variables and formatting mismatches.

> **Proof 1: Pre-commit Hook Failure & Fix**
> *(Paste a snippet of your terminal error here showing ruff/black/mypy failing, followed by the fixed code snippet)*

I corrected the variables and adjusted the logger arguments, which allowed the tests to pass.

Next, I needed to run my `pr-precheck` tool to ensure my PR was ready. However, earlier in the process, I discovered my tool's original logic was too rigid. My strict scope checks were rejecting perfectly feasible real-world issues simply because they weren't perfectly tidy. I had to change my tool's logic by patching it with a `scope-feasible` check.

> **Proof 2: The Scope Patch in `rubric.md`**
> `| **scope-feasible** | plan, issue | The issue is bounded and feasible for a newcomer, even if the repository's scope is slightly messy. | required |`

By updating this rule, the tool became capable of handling open-source unpredictability. When I finally ran `pr-precheck` on my Issue #64 branch, it successfully validated that my diff matched my plan without any unreviewable debris, allowing me to confidently open the pull request.

## Limitations and what's next

While the `pr-precheck` tool is highly effective at catching stated deviations and visible debris, its limitation lies in interpreting the *intent* of commented-out code. My `unreviewable-debris` check currently treats all commented-out lines as a failure. If a PR intentionally comments out code to document an alternative approach for reviewers, the tool will falsely reject it.

To address this, my next step is to update the tool's procedure logic to differentiate between debug debris (like `print()` statements) and structurally sound documentation blocks, possibly by cross-referencing them with explicit developer notes in the PR description.
