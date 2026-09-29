# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: In the repro report header or claim comment, before steps are listed.

What good looks like: Tool versions and OS are explicitly named (e.g., "Python 3.9.2, macOS 14.1"). If the issue targets specific versions, the report either matches them or calls out the difference.

## Steps

Where it lives: In the repro report as a numbered list, starting from "clone the repo" or equivalent.

What good looks like: A stranger could follow them without guessing major setup or invocation details. Each step names the command/action taken and the output observed. Irrelevant details (like exact dependency versions when not related to the issue) may be omitted, but all inputs needed to reproduce should be present.

## Behavior shown

Where it lives: In the repro report as excerpts, logs, or screenshots attached to or quoted in the report.

What good looks like: The artifact directly shows the issue's stated behavior (e.g., if the issue says "duplicate embeddings appear," the output shows duplicates). The excerpt is large enough to verify, not a one-line claim.

## Honesty

Where it lives: In the claim comment (first comment on the issue thread) and the repro report conclusion.

What good looks like: The report says exactly what happened: if steps succeeded, if they failed, or if the issue could not be reproduced. Claims match the evidence (e.g., "I see duplicates" only if duplicates appear in the output shown).

## Comms

Where it lives: The claim comment itself; the repo's stated contribution policy in repo-facts (check for disclosure requirements); any issue templates or communication norms.

What good looks like: The claim comment (1) discloses AI assistance explicitly if ANY text or code came from AI; (2) follows the repo's stated issue template or communication policy; (3) makes no claims unsupported by evidence; (4) avoids language suggesting certainty ("this reproduces the bug") when the evidence only shows a specific output matching the report (not necessarily proving the issue is real in all cases). The comment should be anchored to what was actually observed, not what the observer infers the bug to be.
