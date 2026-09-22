# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/1

**Verdict output**

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/1",
  "checks": [
    {"name": "Repo is actively maintained", "grade": "pass", "evidence": "Last push 2026-09-16, within 3 months"},
    {"name": "Clear, bounded issue", "grade": "pass", "evidence": "Specific bug with root cause: _check_skip() passes string instead of bool; identified files and 4–6 hour effort"},
    {"name": "No AI ban in policy", "grade": "pass", "evidence": "No CONTRIBUTING.md; README discusses AI but imposes no ban"},
    {"name": "Active maintainer presence", "grade": "pass", "evidence": "Commits on 2026-09-16 (6 days ago, within 2 weeks)"},
    {"name": "No existing assignment", "grade": "pass", "evidence": "No assignees, no linked pull requests"}
  ],
  "verdict": "accept"
}

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Run 1: 14/20 (initial rubric too strict)
Run 2: 15/20 (added AI policy check)
Run 3: 16/20 (improved "Clear, bounded issue" check)
Run 4: 17/20 (refined "Active maintainer presence" check)
Run 5: 18/20 (final passing run, matching eval-run.txt)

**Issue analysis**

Issue-11 (zxcalc/zxlive#519): "The rewrite sometimes applies multiple times when clicked on the sidebar"

Gold label: accept
My rubric: accept ✓

My rubric correctly identified this as a good first issue because:
- Clear, reproducible bug: "rewrite applies multiple times, produces large cluster of nodes"
- Active repo: commits on 2026-08-04
- Bounded scope: specific UI behavior, not a vague refactor
- Unclaimed: no assignees or linked PRs
The issue demonstrates that my "Clear, bounded issue" check successfully accepts specific bugs with clear descriptions, not just issues with "good first issue" labels.

**Check rationale**

Check: "Active maintainer presence"

Wording (from rubric.md): "Repo has commits within the last 2 weeks OR a maintainer appears in the first-response sample (even if responses are slow)"

Reasoning: Early versions of my rubric required maintainer comments on every issue within 30 days, which rejected good issues from quiet repos that were still actively maintained (commits happening regularly). This check balances two signals: recent commits show the repo is alive, while the first-response sample shows whether maintainers engage with issues. Either signal indicates an active, welcoming project. This fixed issue-14, a good documentation cleanup in a "quiet but living repo."

**Trade-offs**

This check's trade-off is that it accepts repos where maintainers rarely respond to issues, as long as they commit regularly. This means I might accept an issue from a repo with poor communication practices, where the maintainer merges PRs but doesn't provide helpful feedback. Issue-15 (years of design debate with abandoned PRs) and issue-20 (vague feature wish) were still rejected by other checks, but the "Active maintainer presence" check alone cannot distinguish between a busy maintainer and an unresponsive one. This is acceptable because the other four checks catch most problems; this check's job is only to confirm the repo is not completely dead.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests and time:** I chose Issue #1 because it's a clear, concrete bug in the ingestion pipeline that fits my 4-6 hour availability. The bug is well-scoped — a type mismatch in the _check_skip() function — so I can understand and fix it without getting lost in tangential system design. I'm interested in learning how embeddings work, and fixing a bug in that system is a practical way to do that.

2. **What the verdict identified correctly and what I weighed:** My rubric correctly identified that this issue meets all criteria: the repo is actively maintained, the bug is bounded and reproducible, no one is working on it, and there's no AI policy ban. What the rubric couldn't capture is the repository's code quality and the clarity of its maintainers' feedback style — both of which I assessed by reading the issue thread and the project README. The skill's verdict was accurate for what it was designed to check.

3. **Anticipated difficulty in claiming it:** I expect claiming this issue will be straightforward. The issue description is clear, the expected outcome is specific, and there's an estimated 4-6 hour effort. The main challenge will be setting up the local environment and understanding the embeddings system, but the bug itself seems contained. I don't anticipate architectural disagreements or scope creep since the issue is a bug fix, not a design discussion.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
