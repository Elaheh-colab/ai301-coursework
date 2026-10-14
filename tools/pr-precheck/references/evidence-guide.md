# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives:**

*Eval mode (practice submission):*
- The plan-context block: scope statement and test plan
- The candidate PR's diff: which lines changed
- The candidate PR's description: what the author claims the PR does

*Live mode (your PR):*
- plan.md: your stated scope (files that will/won't change)
- plan.md's Deviations section: any changes from the posted plan
- git diff main...HEAD: your actual changes
- pr_draft.md: your PR title and description

**What good looks like:**

The diff matches the plan's scope exactly. Every changed file falls within the plan's stated boundary. The description claims only what the diff delivers—no "also fixed X" without X in the diff, and no "this is minimal" when the diff is large. Deviation notes in plan.md explain any changes that don't match the posted plan. A description that overstates or understates the scope is silent drift, not a comms problem.

Example from calib-01: Plan says "remove the first (shadowed) file-decoration-style line from themes.gitconfig only". Diff removes exactly one line from exactly that file. Description says "removes the shadowed first... line... rendering is unchanged". ✓ Match.


## Test evidence (harness category: not-tested)

**Where it lives:**

*Eval mode (practice submission):*
- The plan-context block: the test plan (what test was promised?)
- The candidate PR's test-evidence section: before/after output
- The candidate PR's description: reference to test results

*Live mode (your PR):*
- plan.md: your stated test plan (the steps and expected behavior)
- test_evidence.md (from step 11): your before/after test output
- pr_draft.md: your test evidence section in the description

**What good looks like:**

The test evidence is observable: you can see the commands run and the output they produced. The test matches the plan's test plan exactly. Before/after is clear (something failed, now it passes; something was slow, now it's fast; the output changed as expected). The output is actual console output or screenshots, not just "I tested it locally" or "works great". A test that proves nothing observable—like "unit tests pass" without showing which tests or their output—fails this check.

Example from calib-01: Plan promises "re-run the configparser repro, expect clean parse". Test evidence shows: `python3 -c "import configparser..." # before: DuplicateOptionError ... # after: parsed OK`. ✓ Observable and matches plan.

## Diff quality (harness category: unreviewable)

**Where it lives:**

*Eval mode (practice submission):*
- The candidate PR's diff: the unified diff showing all line changes
- The candidate PR's commits: commit messages and the files each touched

*Live mode (your PR):*
- git diff main...HEAD: your full branch diff
- git log main...HEAD: your commit messages
- pr_draft.md: your description of what you changed

**What good looks like:**

The diff is focused: the fix is visible and nothing unrelated rides along. Each commit is atomic (one logical change per commit). No debug statements, commented-out code, temporary logging, or formatting churn. No dead code. No drive-by edits to unrelated files. A reviewer can see exactly what changed and why without hunting through unrelated changes. A large diff with buried changes, or cleanup mixed with the fix, is unreviewable.

Example from calib-01: One commit. Diff shows one line removed from one file. No extra changes. No formatting. Message is clear: "themes: remove shadowed file-decoration-style from gruvmax-fang". ✓ Focused and reviewable.


## Standards and comms (harness category: standards-wall)

**Where it lives:**

*Eval mode (practice submission):*
- The repo-facts block: PR template sections, contribution policy, AI-use disclosure requirements
- The candidate PR's description: whether it follows the template, answers the template's questions
- The candidate PR's title: whether it's clear and follows repo conventions
- The thread highlights: any explicit maintainer direction or policy signals

*Live mode (your PR):*
- The repo's CONTRIBUTING.md: stated requirements and conventions
- The repo's PR template (if it exists): required sections and format
- pr_draft.md: your PR title and description, matching the template
- The issue's thread: maintainer comments or stated direction
- The repo's policy on AI disclosure: whether you disclose if AI was used

**What good looks like:**

The PR description fills the repo's template sections with real content, not boilerplate. If the repo asks for steps to reproduce, you include them. If it asks for expected vs. actual, both are there. The title is clear and follows the repo's naming convention (if stated). If the repo requires AI disclosure and you used AI, you disclose it. Maintainer direction in the thread is engaged—if a maintainer asked a specific question or flagged a concern, the PR description addresses it. A description that ignores the template, leaves sections blank, or dismisses repo conventions fails.

Example from calib-01: Repo has no PR template. Contribution policy asks PRs stay small and reference the issue. PR title references the issue (#2211). Description is concise. Changes are minimal. ✓ Compliant.

