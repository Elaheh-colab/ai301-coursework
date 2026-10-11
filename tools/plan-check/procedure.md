# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the reproduction evidence first (the repro report)
   - Note: what behavior did the repro show? What's the root cause the repro evidence points to?
2. Read the plan comment (the claim that this is what they'll fix)
   - Note: what does the author claim is the problem?
3. Read the plan itself (the full fix description with scope and test strategy)
   - Note: what changes does the plan propose? How will it be tested?

Why this order: The repro evidence is ground truth. You compare the plan against what actually happened, not against what the plan claims happened.

## Evidence gathering

**For diagnosis check:**
- Pull the plan's stated root cause (the "this is the bug" sentence)
- Pull the repro evidence's root cause (what the reproduction report actually identified)
- Record whether they match

**For scope check:**
- Pull the plan's scope statement (the "will change X, won't touch Y" section)
- Record each file named and what the plan says about it
- Note any statements saying what will NOT change

**For test-plan check:**
- Pull the plan's test strategy (the "how we'll verify it works" section)
- Compare against the repro evidence's steps (is the test feasible and observable?)
- Record what the test is and how you could verify it ran

## Check execution

Grade checks in order: diagnosis, then scope, then test-plan, then comms.

For each check:
1. Read the gathered evidence for that check
2. Apply the pass condition from the rubric
3. Grade P (pass), F (fail), or ? (unclear)
4. If evidence is missing (e.g., no test plan mentioned), grade it as ? (unclear)
5. Record your grade and the evidence that decided it

For the comms check specifically:
- If thread highlights are empty, check if the plan comment is honest and clear
- If the repo requires AI disclosure: check if the thread mentions AI; if it does, the comment must explicitly address the AI aspect (disclose using it, or clarify the plan is not AI-assisted)
- If thread highlights name a maintainer's diagnosis or direction, verify the plan comment acknowledges or responds to it

## Verdict assembly

1. Apply the verdict rule: "Ready if all required checks pass. Unclear counts as fail."
2. If all three checks are P: verdict is "ready"
3. If any check is F or ?: verdict is "hold"
4. In the output, quote the evidence from the check that decided the verdict (the blocking check if hold, or any passing check if ready)
