# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis (required) | The plan's stated cause, read against the repro evidence | The plan names the root cause that the reproduction evidence supports; cause matches a specific code location or mechanism shown in the evidence | required |
| scope (required) | The plan's scope statement, naming files or functions that will change | The plan names each file it will change and states what it will not touch; scope is bounded (not "fix the whole module") | required |
| test-plan (required) | The plan's test strategy, compared against the repro evidence's steps | The plan includes how to verify the fix works; test is observable (can be run and verified) and would catch if the fix broke something | required |
| comms (required) | The plan comment read against thread highlights and repo-facts AI policy | The plan comment responds to maintainer guidance in the thread (if any); if the repo requires AI disclosure AND AI is mentioned in the thread, the comment explicitly addresses the AI aspect (either disclosing use or clarifying the plan is not AI-assisted) | required |

## Verdict rule

Ready if all required checks pass. Unclear counts as fail.
