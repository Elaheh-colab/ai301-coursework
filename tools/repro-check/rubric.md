# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded (required) | Environment block in the repro report | Report names the tool version and operating system | required |
| steps-complete (required) | Step-by-step instructions in the repro report | A stranger could re-run the steps without guessing the input, command, or setup | required |
| behavior-matches-issue (required) | Output shown in the repro report vs. the issue description | The observed output matches the issue's described failure, OR the report honestly states the issue could not be reproduced and claim/report agree on that | required |
| outcome-honest (required) | Claim comment and the repro report's conclusion | The report's conclusion that the bug was reproduced is actually supported by the shown output | required |
| disclosure-comms (required) | Claim comment against issue thread and repo's stated conventions/templates | Claim comment follows repo's stated issue template or communication conventions if they exist; any AI-generated text or code is explicitly disclosed; language avoids overconfident claims without full evidence; any promises or commitments are realistic and backed by the report content | required |

## Verdict rule
Accept if all required checks pass. Unclear counts as fail.
