# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

All recency thresholds below are measured against the bundle's stated
capture date, not against today.

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer Alive | repo-facts block: the "last 5 default-branch commits" list (dates and author names), and the "maintainer first-response sample" | At least one of the 5 most recent default-branch commits is dated within 90 days of the capture date and reflects human activity. A commit authored by a bot (username ending in `[bot]`, or a `*-bot` service account) counts as human activity when its message shows it merged a person's pull request (e.g. "Merge pull request #123 from alice/fix-docs"); a bot's own routine upkeep, such as a version bump or a leaderboard refresh, does not. Judge the repo, not this issue: an issue with no maintainer reply still passes when the commit list is live. Use the first-response sample only to break a tie when commit recency is borderline. | required |
| Repo in Use | repo-facts block: the repo line (stars, `archived:`), "latest release", "last push to any branch" | The repo is not archived, AND either the last push to any branch is within 90 days of the capture date or a release was published within 365 days of it. | required |
| Newcomer Scope | issue body, labels, opener's author_association, comment count | Fails if ANY of these hold: (a) the issue is an umbrella or tracking issue — its body is mainly a list of references to other issues or PRs (issue numbers or links), or it explicitly calls itself a tracking, umbrella or mega issue, or it asks for an ongoing program applied repeatedly across the codebase with no defined endpoint ("incrementally add X", "PRs welcome big and small"); (b) the thread exceeds 40 comments, indicating a design still being argued or repeated failed attempts; (c) the issue carries no labels at all AND its opener is not an Owner, Member, or Collaborator, meaning no maintainer has triaged it. Otherwise passes. A short enumerated list of similar, small, concrete items within one feature area ("missing previews for remove identity, fuse spiders, remove self loops") is one bounded deliverable, not an umbrella: grade the size of the work asked for, not the brevity of the writeup. A multi-part but well-specified task with a single coherent deliverable passes, and age alone never fails: a well-labelled issue open for years can still be a good first issue. | required |
| Unclaimed Status | comment thread, issue body | The issue has no assignee, no linked open PR, and no active claim by a maintainer. Per Path Review house rules, other students' claim comments do not block the issue. | required |
| Contribution Policy | repo-facts block: the "contribution policy" line | The policy does not ban, or explicitly advise against, AI-assisted contributions of the kind this issue calls for. Silence passes ("no stated policy", "no statement on AI"). Conditions pass — disclosure, testing, human review, and "you are responsible for your contributions" are terms to follow, not bans. An outright ban ("we do not accept AI-generated code") fails. | required |
| Technical Fit | issue body | The issue aligns with the Python, Streamlit, or ChromaDB skillsets outlined in the fit profile. | preferred |

## Verdict rule

Accept the issue if every required check passes. The preferred checks do not alter the final verdict and are solely used to rank the accepted issues. Any unclear result on a required check is treated as a fail.

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
