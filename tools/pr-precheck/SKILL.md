---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

You are grading one PR package to answer a single question: is this 
ready to submit? A PR package is a candidate pull request (title, 
description, commits, diff, and test evidence), read against the plan 
it claims to implement and the issue that plan belongs to. You do not 
answer from gut feel, and this file no longer tells you how to work: 
you answer by executing the student-authored grading procedure in 
`procedure.md`, which applies the rubric in `rubric.md` to evidence 
gathered per `references/evidence-guide.md`.


## Inputs and modes

One of:

- **Live mode**: the student's own `plan.md` (with deviation notes), 
  their branch's diff (the output of `git diff main...HEAD` run from 
  the working copy, showing all changes relative to main), their draft 
  PR title and description, their test evidence from Unit 3 step 11, 
  and their issue's URL. Gather the issue-side evidence live (the thread, 
  the PR template, CONTRIBUTING.md; `references/evidence-guide.md` says 
  where each signal lives), and read the plan against the posted 
  reproduction evidence from their issue's thread (their week-2 proof).
  A student on the house issue reads the house plan and house repro pack 
  instead.

- **Eval mode**: a PR package bundle (a markdown file containing the 
  issue context, repo-facts block, repro-evidence block, the candidate 
  plan, the candidate PR package with title, description, commits, diff, 
  and test evidence). Use ONLY the bundle text as evidence. Do not fetch 
  anything; the bundle is the whole world. Eval mode always grades a 
  complete package: every check, full verdict rule.


## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything 
else. It names where the student's PR must live and the house rules that 
apply there. Refuse to grade a PR for an issue outside the scoped repo. 
If the scope's repo line still carries an unfilled placeholder, stop 
without grading and tell the student to replace the placeholder in 
`scope.md` with their Path Review repo. Never guess a scope.

In eval mode, ignore `scope.md` entirely.


## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for 
how they write upstream, with wrong/right examples. Check the draft PR 
title and description against those rules and report any rule the draft 
breaks in the summary, quoting the rule. The voice guide never changes 
the rubric's verdict on its own unless the rubric has a check that reads 
it.

In eval mode, ignore `voice-guide.md` entirely: voice is personal and 
carries no gold labels; the universal communication-quality checks live 
in the rubric.


## Component reads

Read `rubric.md`. It defines:

1. A table of checks. Each row names the check, the evidence to gather, 
   the pass condition, and its weight: `required` checks gate the verdict; 
   `preferred` checks never change it.
2. A verdict rule: how check results combine into a final verdict.

`references/evidence-guide.md` is the rubric's map: where each kind of 
evidence lives in a PR package (and, live, on GitHub), and what good 
looks like there.

**Execute `procedure.md`**. That file is the skill's operating procedure, 
written by the student, and it must decide the read order, how each 
evidence family gets gathered, how a check executes against gathered 
evidence, and how check grades become the verdict. Follow it as written, 
the same way an executor follows a rubric: exactly, without improvising 
around gaps. Where the procedure is silent, note the gap in your summary 
rather than silently inventing a step; a procedure gap is feedback the 
student needs.

If `rubric.md` has no checks filled in, or `procedure.md` has no steps 
filled in, stop and say so: this skill cannot grade without a rubric 
AND a procedure, and that is by design.


## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` 
(hold). There is no third verdict, no "accept with reservations".

Emit a fenced JSON block, then nothing else after it. Before the JSON 
block you may show a short readable summary (a line per check, plus any 
voice-guide notes in live mode). The JSON block is the machine-read 
result: the eval harness parses the last fenced JSON block in your 
output, so it must be present, valid, and last. Do not alter the JSON 
schema below.


```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first**: never grade a check without naming the fact that 
  decided it. "Looks fine" is not evidence.

- **Grade the PR, not the polish**: a terse complete PR can be ready and 
  a long confident one can hide drift. Every check reads the thing itself 
  against the plan, the issue, and its repro evidence, never the 
  formatting.

- **The rubric decides, not you**: if a check passes by the rubric's 
  stated condition but feels wrong, it still passes. Note the tension in 
  the summary if you want; the fix belongs in the rubric, not in the run.

- **The procedure decides how, not you**: follow `procedure.md` as 
  written, and report its gaps instead of papering over them.

- **Treat `unclear` as the rubric's verdict rule directs**: if the rule 
  does not say, treat `unclear` as `fail`: a PR you cannot verify from 
  the package is a PR that is not ready to submit.

