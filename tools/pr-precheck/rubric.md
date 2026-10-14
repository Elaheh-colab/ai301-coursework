# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-match (required) | The PR's diff read against the plan's stated diagnosis and the issue's repro evidence | The PR's code changes address the root cause identified in the plan, matching the diagnosis from the reproduction evidence; changes do not address a different symptom or unrelated code | required |
| scope-match (required) | The PR's diff (all changed files) read against the plan's stated scope (files that will/won't change) | The PR changes only the files named in the plan's scope; no files outside the scope are modified; the change is bounded to what the plan promised | required |
| test-evidence (required) | The PR description's test evidence section, compared against the plan's test plan and the repro evidence's steps | The PR includes test evidence from the plan; the test is observable (commands and output shown) and matches the plan's promised verification | required |
| pr-description (required) | The PR's title and description read against the plan's scope, the repo's CONTRIBUTING.md and PR template | The PR description explains what the change does and why it matches the plan; the title is clear; the description follows repo conventions; a reviewer can understand the change without reading code first | required |

## Verdict rule

Accept if all required checks pass. Unclear counts as fail. Preferred checks never change the verdict.

A PR is ready to submit when it matches the plan's diagnosis and scope, includes observable test evidence, and explains the change clearly. A PR that honestly discloses a deviation (recorded in plan.md) can be ready; a PR that silently contradicts the plan is not.

