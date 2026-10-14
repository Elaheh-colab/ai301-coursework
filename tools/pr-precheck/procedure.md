# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. Read the plan.md first (the plan as posted, with any deviations noted)
   - Note: What does the plan say will change? What scope did it promise? What test did it promise?
2. Read the PR's diff (output of `git diff main...HEAD`)
   - Note: What files actually changed? How much did they change?
3. Read the test evidence (from the PR description)
   - Note: What test was run? What does the output show?
4. Read the PR's title and description
   - Note: How does the author explain the change? Does it match the plan?

Why this order: The plan is ground truth. You compare the PR against what was promised, not against what the PR claims it did.

## Evidence gathering

**For plan-match check:**
- Pull the plan's stated diagnosis (what root cause does it name?)
- Pull the PR's diff (what does it actually change?)
- Pull the issue's repro evidence (what behavior did the reproduction show?)
- Record: does the diff address the diagnosed root cause, or something else?

**For scope-match check:**
- Pull the plan's scope statement (which files will/won't change?)
- Pull the PR's diff (which files actually changed?)
- Record: are all changed files within the planned scope? Any changes outside scope?

**For test-evidence check:**
- Pull the plan's test plan (what test was promised?)
- Pull the PR description's test evidence section (what test was actually run?)
- Record: is the test observable? Does the output show it was run? Does it match the promised test?

**For pr-description check:**
- Pull the PR's title and description
- Pull the plan (what should the PR explain?)
- Pull the repo's CONTRIBUTING.md and PR template (what standards apply?)
- Record: does the description explain the change clearly? Does it follow repo conventions? Can a reviewer understand the change?


## Check execution

Grade checks in order: plan-match, then scope-match, then test-evidence, then pr-description.

For each check:
1. Read the gathered evidence for that check
2. Apply the pass condition from the rubric
3. Grade P (pass), F (fail), or ? (unclear)
4. If evidence is missing or cannot be verified, grade it as ? (unclear)
5. Record your grade and the evidence that decided it

**For plan-match check specifically:**
- Compare the PR's diff against the plan's diagnosis
- Does the diff address the root cause named in the plan?
- If the diff fixes something other than the diagnosed cause, it fails

**For scope-match check specifically:**
- Compare the files in the PR's diff against the plan's scope
- Does every changed file fall within the plan's stated boundary?
- If any file outside scope was changed, or in-scope files were not changed as planned, check for honest deviation notes in plan.md

**For test-evidence check specifically:**
- Compare the test evidence in the PR against the plan's promised test
- Is the test observable (can you see the commands and output)?
- Does the output show the test actually ran?
- If evidence is missing entirely, grade unclear

**For pr-description check specifically:**
- Read the title and description as a reviewer would
- Can you understand what the change does without reading code?
- Does it follow the repo's PR template and contribution standards?
- If the description is vague or ignores repo conventions, it fails


## Verdict assembly

1. Apply the verdict rule: "Accept if all required checks pass. Unclear counts as fail."
2. Grade the checks:
   - If all 4 checks are P (pass): verdict is "accept"
   - If any check is F (fail) or ? (unclear): verdict is "reject"
3. In the output, quote the evidence from the check that decided the verdict:
   - If accept: quote any one passing check's evidence
   - If reject: quote the evidence from the check that failed (the blocking check)
4. Remember: a PR that honestly discloses deviations in plan.md can still be ready if the code matches the updated plan

