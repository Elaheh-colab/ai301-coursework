# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**Where it lives (eval package):**
- The repro evidence's "Actual:" section (what the reproduction showed)
- The candidate plan's "Cause:" section (what the plan says is wrong)
- The candidate plan comment (how the cause connects to the evidence)

**What good looks like:**
The plan's stated cause names a specific mechanism or code location that the repro evidence actually shows. The cause is not speculation ("probably in the editor code") but a grounded claim ("`HashedEventRegister` drops the default bindings" after the evidence measured which bindings are missing). The cause explains the observed behavior — not a different symptom, not the symptom dressed as a cause.

## Scope

**Where it lives (eval package):**
- The candidate plan's "Change:" or "Scope:" section, with explicit "In scope:" and "Out of scope:" or "Not in scope:" lines
- File names or function names mentioned in the plan
- Statements about what will or will not be touched

**What good looks like:**
The plan names each file it will change and states what it will not touch. Scope is bounded: "add one check in output.rs" or "modify the refresh callback in sync_controller.go", not "fix the whole module" or "refactor the editor". A reader can point to exactly which files and functions will change.

## Executability

**Where it lives (eval package):**
- The candidate plan's "Changes:" or implementation section
- The candidate plan comment's description of the work

**What good looks like:**
The plan states not just the goal but the concrete steps: which file, which function, which lines. "Call `generate_default_bindings()` before registering custom bindings" is executable; "figure out where the undo history lives" is exploration, not a plan. A stranger could start coding from the plan without asking the author questions.

## Test plan

**Where it lives (eval package):**
- The candidate plan's "Test plan:" or "Test:" section
- The candidate plan comment's reference to how the fix will be verified
- The repro evidence's "Steps:" section (as a baseline for comparison)

**What good looks like:**
The plan includes how to verify the fix works, and the test is observable (can be run and verified). "Repro steps: at step 3 the color must flip without leaving the view" is observable; "undo works after toggling" is not. A decisive test names what to check and what the expected outcome is, and would catch if the fix broke something (e.g., "verify search bindings work" catches side effects from the binding registration change).

## Honesty

**Where it lives (eval package):**
- The candidate plan or plan comment's statements about unknowns, risks, or caveats
- Admissions of limits (e.g., "haven't looked at the pager code yet")
- Deviations from the diagnosis (e.g., "this might also help with X")

**What good looks like:**
Stated unknowns are genuine. "My plan is to poke around the editor code this weekend and figure out where it lives" is honest uncertainty; "probably handled somewhere in the editor code" dressed as a plan is false confidence. The plan does not overstate confidence — it says what is known from evidence and what requires investigation.

## Comms

**Where it lives (eval package):**
- The candidate plan comment (tone, responsiveness to the issue and thread)
- The repo facts' contribution policy (whether AI disclosure is required)
- The thread highlights (any signals from maintainers about diagnosis, direction, or policy; whether AI is mentioned)

**What good looks like:**
The plan comment responds to the thread context. If the thread highlights a maintainer's diagnosis or direction, the comment acknowledges it. **If the repo requires AI disclosure AND the thread mentions AI**, the comment explicitly addresses the AI aspect—either disclosing AI use ("I used Claude to explore...") or clarifying the plan is not AI-assisted ("The thread discussed an AI proposal, but I'm following your human direction instead..."). The comment is in the author's voice, not boilerplate. A comment that ignores maintainer guidance OR fails to address AI when the repo requires it and the thread mentions it fails this check.
