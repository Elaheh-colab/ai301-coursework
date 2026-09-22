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

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repo is actively maintained | Last 5 commit dates on default branch OR latest release date in repo-facts | At least one commit within the last 3 months OR a release within the last 3 months | required |
| Clear, bounded issue | Issue title, description, and labels | Issue is a specific bug or feature request with clear problem statement (not a vague refactor, years-long design debate, or spec-less wish); labels like "bug", "good-first-issue", or "documentation" are helpful signals | required |
| No AI ban in policy | Contribution policy in repo-facts block | Policy does not explicitly ban AI-generated code or documentation | required |
| Active maintainer presence | Last 5 commit dates on default branch OR maintainer first-response sample | Repo has commits within the last 2 weeks OR a maintainer appears in the first-response sample (even if responses are slow) | required |
| No existing assignment | Assignees and linked PRs in repo-facts | No current assignees AND no open linked PRs | required |


## Verdict rule
Accept if all five required checks pass. Unclear counts as fail.
<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
