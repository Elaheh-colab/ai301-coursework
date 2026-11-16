# Contribution: A finding never says how its group score was aggregated, or whether a number is absolute

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Elaheh Baharlouei
**GitHub Username:** Elaheh-colab
**Issue:** https://github.com/wehnsdaefflae/llmsectest/issues/37

**Pull Request:** https://github.com/wehnsdaefflae/llmsectest/pull/43

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and patched issue-scout's search strategy and rubric**

I built issue-scout's search strategy: two `gh search issues` queries, a fit profile, and ranking filters that drop assigned and stale issues, then graded the top results. The first scan fell short: only one query ran, the maintainer check counted repo-owner commits instead of responses, and the rubric passed issues it should have rejected, including #519, whose body banned coding agents from the completing PR. I patched the rubric to require owner or collaborator comments within 30 days, read issue bodies for AI bans, and limit bounded issues to two named files, then re-ran the scan with a pytest query and logged each change in scan-notes.md.

**Unit 6: Installed the voice guard and wrote a repo memory file**

I merged my three voice guides into one, added an Upstream section for claims, questions, and pings, installed the voice-guard hook, and wrote a 30-line CLAUDE.local.md for my llmsectest clone, kept out of git with .git/info/exclude. The guard fell short twice: it couldn't run until I put `claude` on my PATH, and it blocked my claim draft twice because the draft gave a first step but never said what I planned to change. I rewrote the draft to state the plan, the first step, and a date, and it passed. I did not post it, because the maintainer had already assigned me the issue and the guard cannot see an existing claim.


**Unit 7: Installed the ship-gate and wrote my gate manifest**


I installed the ship-gate and wrote a manifest of three checks taken from the project's CI and CONTRIBUTING.md (`ruff check`, `coverage run -m pytest -q`, `coverage report`), using the venv's own tools so they run in a fresh terminal. The gate passed my branch every time, but its pr-precheck notes kept finding real problems: a stale 1059 test count in my description (main collects 1070), no environment or deviation note, and a title with no issue number. I fixed each of them before opening the PR. What stopped me was my tokens, not the gate: a fine-grained token could not push to my fork or open a PR on the maintainer's repo, so I added Contents and Pull requests permissions and then switched `gh` to a classic token, and I re-ran the gate because its PASS only lasts 30 minutes.


**Unit 8: Ran the PR monitor on my PR and drafted my playbook**

I filled in my playbook (response rules, a 3-day staleness threshold from five merged PRs, one nudge, and walk-away criteria), then ran the monitor on PR #43. It drafted a wait note, since the PR was under a day old with no replies, and I didn't post it: I decided to wait and check each run. I hit a PATH problem because the monitor calls the Claude CLI, which I fixed by prefixing the command with `PATH="$HOME/.local/bin:$PATH"`. A rule I'd write differently is the nudge: I'd keep the threshold, but ask for a review rather than a yes or no on the open question.

---

## Why I Chose This Issue

I found #37 on the Issue Selection site, filtering for Python and backend work to match my fit profile, and I also searched GitHub with issue-scout's strategy: two `gh search issues` queries and ranking filters that drop assigned and stale issues. The first scan accepted five candidates, but on closer reading one of them, #519, reserved its issue for outside contributors and the rubric had missed it, so I patched the rubric and re-ran the scan. I graded two llmsectest issues, #35 and #37. Under the first rubric, #35 was accepted and #37 was rejected on the bounded-scope check, because it names three report files and the rule allowed two. After I replaced that check with a scope-feasible check, #37 passes on scope, and its difficulty note is moderate: the change touches `statistics.py`, `sarif_generator.py`, and `console_summary.py`. The re-grade on 2026-11-14 still rejects it, but only because its "No existing assignment" check fails on an issue I hold myself; the rubric has no exception for that, and I logged the gap in scan-notes.md.

I chose #37 because the fix adds one labeled field to the reports, it has less overlap with other work than #35 (which touches the LLM10 detector that PR #22 changed recently), and it fits my profile: Python, writing a test for existing behavior, and reading an unfamiliar codebase's reporting path. I hope to learn how a report's aggregation is computed end to end, and how to write a test that keeps a label tied to the code it describes. My claim comment is at https://github.com/wehnsdaefflae/llmsectest/issues/37#issuecomment-6729558550. On 2026-11-09 the maintainer, wehnsdaefflae, assigned the issue to me and asked that the aggregation name come from the function itself.

An honest read of the scout: it fell short in several ways. The maintainer check counted repo-owner commits instead of responses, it ignored claim comments and reservations in issue bodies, its file-count rule rejected a reasonable issue, and it rejects an issue assigned to me. I patched the first two, replaced the file-count rule with the scope-feasible check, and recorded each change, including the self-assignment gap, in scan-notes.md.

**Toolkit**

- Tool: issue-scout, with my own search strategy (two `gh search issues` queries and ranking filters) and my own rubric. I ran scans, then graded my picks directly by URL.
- What it produced: scan results and direct grades for #35 and #37. After the scope patch, #37 passes on scope with a "moderate" difficulty note, but the scout still rejects it on the no-existing-assignment check.
- Difficulties: it counted repo-owner commits as maintainer activity, ignored claim comments and reservations in issue bodies, rejected a reasonable issue on a file-count rule, and rejects an issue assigned to me; the first scan also ran only one query.
- What changed: patched the maintainer check to require owner or collaborator comments within 30 days, added issue-body reads for AI rules, replaced the file-count check with scope-feasible plus a difficulty note, switched the query to pytest, and logged the self-assignment gap without changing the rule.
  
---

## Understanding the Issue

**Problem Description**

llmsectest reports publish aggregated numbers: a score per OWASP category, a severity score, and an overall risk score. They never say how those numbers were combined, so two reports built with different aggregation look identical.

**Expected Behavior**

Each aggregated score in the report names the function that produced it, in the report file itself and in the terminal summary. The name comes from the function, so the label cannot drift away from the code.

**Current Behavior**

The offline demo run's JSON summary has a `risk_assessment` block with `overall_score`, `category_scores`, and `severity_scores` and no field naming how they were computed. `grep -i aggregat` over the reports finds nothing.

**Affected Components**

`src/llmsectest/reporting/risk_scorer.py` (computes the scores), `json_summary_generator.py` (writes `risk_assessment`), `console_summary.py` (prints the risk score), and the tests in `tests/test_core_modules.py` and `tests/test_report_formats.py`.

**Toolkit**

- Tool: Claude Code with my `CLAUDE.local.md` memory file, after one scoped orientation run over `src/llmsectest/reporting/`.
- What it produced: a map of where the scores are computed and written, and the flow from results through statistics and the risk scorer to the generators.
- Difficulties: the issue says group scores are computed in `statistics.py`, but that file only holds counts, and the orientation found no "group" concept. The real scores are in `risk_scorer.py`.
- What changed: I recorded the mismatch and an open question for the maintainer in `CLAUDE.local.md`, and I based my plan on `risk_scorer.py`.

---

## Reproduction Process

**Environment Setup**

macOS 15.7.3, Python 3.14.5 in a venv (`test-issue`), llmsectest 0.4.1 installed from my clone at commit `9a62aa8` (2026-11-06) with `pip install -e ".[dev,cvss]"`. No challenges setting up the project: the install and the offline demo ran on the first try, and `coverage run -m pytest -q` passed all 1059 tests.

**Steps to Reproduce**

1. Clone my fork, check out commit `9a62aa8`, create and activate a venv, and install with `pip install -e ".[dev,cvss]"`.
2. From the repo root, run the offline demo scan: `python -m llmsectest --report-formats=sarif,json`. It writes `results/demo-vulnerable.sarif` and `results/pytest-summary.json`.
3. Search both reports for an aggregation name: `grep -n -i "aggregat" results/*.json results/*.sarif`.
4. Observed result: the grep prints nothing, and the `risk_assessment` block (line 2140 of `results/pytest-summary.json`) holds `overall_score`, `category_scores`, and `severity_scores` with no field naming how they were combined.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:**
  ```
  $ grep -n -i "aggregat" results/*.json results/*.sarif
  (no output)

  results/pytest-summary.json:2140:  "risk_assessment": {
  results/pytest-summary.json:2141:    "overall_score": 70.07156794425087,
  results/pytest-summary.json:2144:    "category_scores": {
  ```
- **My findings:** the report states scores but never names the function that aggregated them, which matches what the issue describes. I have not yet checked the console output or the HTML and Markdown reports, and I still need to confirm with the maintainer which scores should carry the name.

**Toolkit**

- Tool: repro-check, in live mode, run on my repro report and my claim draft together.
- What it produced: an accept verdict with every check passing, plus voice-guide notes on the claim draft.
- Difficulties: it noted there was no explicit clone-and-checkout step in my report, and that my claim draft is redundant because the maintainer had already assigned me the issue.
- What changed: I added a clone-and-checkout step to the steps above, and I did not post a second claim.


---

## Solution Approach

**Analysis**

Three scores in `risk_assessment` are produced by inline arithmetic with no recorded name. `category_scores` come from `_calculate_category_scores` (risk_scorer.py, line 169: failure rate x 100 x a per-category multiplier, capped at 100). `severity_scores` come from `_calculate_severity_breakdown` (line 354: failure rate x 100 x weight/10 per severity, capped at 100). `overall_score` comes from the weighted sum in `calculate_risk` (line 97: 0.30 failure score + 0.25 severity impact + 0.20 mean category score + 0.15 trend + 0.10 baseline). `_calculate_severity_score` (line 147) only feeds the severity-impact term of the overall score; it does not fill `severity_scores`. The `RiskScore` dataclass has no field for how scores were computed. `JSONSummaryGenerator.generate` copies the `RiskScore` fields into `risk_assessment`, and `console_summary.py` prints the overall score, so no surface can state the aggregation. `statistics.py` and the SARIF tally hold counts, not scores, so they have no aggregation to name.

**Proposed Solution**

Extract the three calculations above into three small named functions in `risk_scorer.py`, each taking its weights as arguments and returning exactly what the code returns today. The names describe the math, for example `capped_scaled_failure_rate`, `weight_scaled_failure_rate`, and `weighted_factor_sum`. Add an `aggregations` mapping to `RiskScore`, filled from the `__name__` of the function that actually produces each score (`category_scores`, `severity_scores`, `overall_score`), so the report asks the function for its name (the maintainer's guidance on #37). The overall name covers the final weighted sum, not its inputs. Copy the mapping into `risk_assessment` in the JSON summary and print one line in the console summary. I am not changing the scoring results, the SARIF tally, `statistics.py` (counts only, no scores), the HTML and Markdown reports, or the issue's other two fields (absolute versus relative scores, and what a severity is a severity of), which the issue says belong in separate PRs.

**Implementation Plan**

1. Ask the maintainer whether extracting named functions is welcome. Default if no answer: name `category_scores`, `severity_scores`, and `overall_score`.
2. Before changing code, record the demo run's `risk_assessment` scores, so I can show they are identical afterward.
3. Write the failing test first in `tests/test_core_modules.py`: `RiskScore.aggregations` maps each of the three scores to the `__name__` of the function that fills it, and that function's output on known statistics equals the score in the report. It fails before the fix because the field does not exist.
4. In `risk_scorer.py`, extract the three functions and add the `aggregations` field. The existing score tests must pass unchanged.
5. In `json_summary_generator.py`, copy it into `risk_assessment`. A test in `tests/test_report_formats.py` asserts `risk_assessment["aggregations"]["category_scores"]` equals the function's `__name__` in a generated summary.
6. In `console_summary.py`, print one line stating the aggregation. A console summary test asserts that line contains the function's name.
7. Run the manifest checks (`ruff`, `coverage run -m pytest -q`, `coverage report`), and add a `CHANGELOG.md` bullet under `[Unreleased]`.

Deviations from this plan will be recorded here as they happen.

2026-11-15: Plan step 3 asked the test to also check each function's output against the reported score; the tests check the names, and the existing score tests plus the unchanged demo scores cover the values. Plan step 1 (asking the maintainer first) was not done; the question is in the PR instead.



**Toolkit**

- Tool: plan-check, in live mode, run on my plan.md and my draft plan comment together, three times.
- What it produced: two rejects and then an accept. The first said the diagnosis was unclear because no repro comment was posted on the issue; the second failed the diagnosis because I tied `severity_scores` to the wrong function.
- Difficulties: my first plan would have labeled `severity_scores` with a function that never fills that field, and the labels would have read as private method names. The skill also expects a repro comment on the thread, which this step says not to post, and its procedure says ready/hold while its output says accept/reject.
- What changed: I revised the plan to extract named functions, mapped each score to the function that actually fills it, put the real grep output and versions in the comment, and added why the SARIF tally and `statistics.py` are out of scope.

---

## Testing Strategy

I re-ran my reproduction on main and on my branch. On main, `grep -n -i "aggregat" results/*.json results/*.sarif` prints nothing, `risk_assessment` has no `aggregations` key, and the console risk section ends at the Confidence line. On my branch the same steps find `"aggregations"` in the JSON with `capped_scaled_failure_rate`, `weight_scaled_failure_rate`, and `weighted_factor_sum`, and the console prints an `Aggregation:` line with the same names. The overall, category, and severity scores are identical before and after (overall 70.07156794425087).

Three new tests each failed before their fix: on the `RiskScore` object (`AttributeError: ... no attribute 'aggregations'`), in the JSON summary (`KeyError: 'aggregations'`), and in the console summary (the function name was not in the output). Then I ran the repo's own checks from my manifest on the branch: `ruff check src tests examples` passes, `coverage run -m pytest -q` passes all 1073 tests (1070 on main before my change), and `coverage report` totals 88%. The full output is in `test_evidence.md`.


**Toolkit**

- Tool: my ship-gate manifest (`ruff check`, `coverage run -m pytest -q`, `coverage report`), run by hand on the branch, plus the demo scan from my reproduction. The gate itself runs the same commands when I open the PR.
- What it produced: before and after output for the reproduction, three failing-first tests, and clean manifest checks, collected in `test_evidence.md`.
- Difficulties: plain `pytest` fails one unrelated test (`test_llm08_fixture_design.py`, `No module named 'tests'`) on main as well as on my branch, because it only imports under `python -m pytest`.
- What changed: I used the project's own `coverage run -m pytest -q` as the test command everywhere, and confirmed the failure also happens on main.

---

## Implementation Notes


**2026-11-15**

Made the branch `feat/37-name-score-aggregation` and wrote the failing test first: it expects `RiskScore.aggregations` to name the function behind each score, and it failed with `'RiskScore' object has no attribute 'aggregations'`. Then I extracted the three score calculations in `risk_scorer.py` into named functions (`capped_scaled_failure_rate`, `weight_scaled_failure_rate`, `weighted_factor_sum`), added the `aggregations` field to `RiskScore`, and confirmed the demo run's overall, category, and severity scores are identical to the ones I recorded before the change. `coverage run -m pytest -q` passes (1071 tests) and `ruff check` is clean.

**2026-11-15**

Wrote `aggregations` into the JSON summary's `risk_assessment`. The test failed first with `KeyError: 'aggregations'`; after the one-line change in `json_summary_generator.py`, the demo run's report shows `capped_scaled_failure_rate`, `weight_scaled_failure_rate`, and `weighted_factor_sum`, and the scores are unchanged. `coverage run -m pytest -q` passes (1072 tests).

**2026-11-15**

Printed an `Aggregation:` line under the console risk score (the test failed first because the function names were not in the output) and added a CHANGELOG entry under Unreleased, `### Added`. All 1073 tests pass and `ruff check` is clean. One deviation from my plan: I did not ask the maintainer a question first (step 1), because the maintainer's earlier note on #37 already said the function should be the single source of the name; I will raise the question about the other scores in the PR instead.

**2026-11-15**

Opened PR #43 against `wehnsdaefflae/llmsectest`. The push to my fork failed with a 403 and `gh pr create` failed with a token error, because my fine-grained token had no Contents or Pull requests permission and cannot open a PR on another person's repo. I added the permissions to push, then switched `gh` to a classic token with the `repo` scope, ran `gh repo set-default wehnsdaefflae/llmsectest`, re-ran the ship-gate, and opened the PR through Claude Code.

**2026-11-15**

Filled in my PR-monitor playbook (a 3-day threshold from five merged PRs) and ran the monitor on PR #43. It drafted a wait note, because the PR was under a day old with no replies, and I did not post anything. The monitor needed `PATH="$HOME/.local/bin:$PATH"` to find the Claude CLI.


**Toolkit**

- Tool: Claude Code with my `CLAUDE.local.md` memory file, writing each test first and then the fix, one commit per plan step.
- What it produced: four commits on `feat/37-name-score-aggregation`: the named functions and `RiskScore.aggregations`, the JSON summary field, the console line, and the CHANGELOG entry.
- Difficulties: ruff flagged missing blank lines after my first edit, two edits left stray blank lines in the diff, and I skipped plan step 1 (asking the maintainer a question) because the maintainer's earlier note already covered it.
- What changed: I fixed the spacing before committing, and recorded the skipped step as a deviation in my Implementation Notes entry.


---

## Pull Request

**PR Link:** https://github.com/wehnsdaefflae/llmsectest/pull/43

**PR Description:** The PR extracts the arithmetic behind the three risk scores in `risk_scorer.py` into named functions (`capped_scaled_failure_rate`, `weight_scaled_failure_rate`, `weighted_factor_sum`), adds `RiskScore.aggregations` filled from each function's own `__name__`, writes it into the JSON summary's `risk_assessment`, and prints one `Aggregation:` line under the console risk score. The scores are unchanged. The description shows the before and after output from the demo scan, the three tests that failed before their fix, and the passing checks (ruff clean, 1073 passed against 1070 on main, 88% coverage). It says what I left out (`statistics.py`, the SARIF tally, the HTML and Markdown reports, and the issue's other two fields), discloses what Claude Code did, records two deviations from my plan, says `Fixes #37`, and asks the maintainer whether the aggregation should be named in `statistics.py` and `sarif_generator.py` too.


**Maintainer Feedback:**

- 2026-11-15: none yet.

**Status:** Awaiting review (waiting on the maintainer)

**Toolkit**

- Tool: the ship-gate, a hook that runs my manifest checks (`ruff`, `coverage run -m pytest -q`, `coverage report`) and then my pr-precheck on my branch, plan, evidence, and description before `gh pr create`.
- What it produced: four runs, all PASS. Each pr-precheck read-out also listed real fixes: the stale 1059 test count in my description (main collects 1070), the missing environment and deviation note, and a title with no issue number.
- Difficulties: the PASS only lasts 30 minutes, so I had to re-run it after a token problem. My fine-grained token could not push to my fork or open a PR on someone else's repo.
- What changed: I corrected the description, `plan.md`, and the title, and switched `gh` to a classic token with the `repo` scope. I also ran `gh repo set-default wehnsdaefflae/llmsectest` so the PR went to the original repo.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned to trace where a number comes from in an unfamiliar codebase, using `grep` and by reading the functions that compute it, and to write the failing test first so each change has proof. I used git branches and small commits that each say what they do, and pushed to a fork. I also learned to run a project's own checks (`ruff check`, `coverage run -m pytest -q`) and read the coverage output. On the tooling side, I built and patched a scout rubric, a voice guard, a ship-gate manifest, and a PR-monitor playbook.

**Challenges Overcome**

The hardest parts were not the code. My voice guard blocked my claim draft twice until it said what I planned to change, and plan-check rejected my plan twice, the second time because I tied `severity_scores` to the wrong function. Pushing my branch failed with a 403 and opening the PR failed with a token error, because my fine-grained token had no Contents or Pull requests permission and cannot open a PR on someone else's repo; I fixed it by adding permissions and then switching `gh` to a classic token. The `claude` command was also missing from my PATH several times, and my scout rejected issue #37 only because the maintainer had assigned it to me, which I chose to keep.

**What I'd Do Differently Next Time**

I would check my token's permissions before my first push, and read each function that fills a score before writing the plan, so the label cannot name the wrong one. I would measure test counts on main myself instead of reusing an old number (I wrote 1059 when main had 1070). 

---

## Resources Used

- Issue #37 and the maintainer's guidance on it, that the function should be the single source of the name: https://github.com/wehnsdaefflae/llmsectest/issues/37
- My PR and its CI checks, which showed the tests passing: https://github.com/wehnsdaefflae/llmsectest/pull/43
- The repo's CONTRIBUTING.md and PR template, for the failing-test rule and the checklist: https://github.com/wehnsdaefflae/llmsectest/blob/main/CONTRIBUTING.md
- `src/llmsectest/reporting/risk_scorer.py`, where the three scores are computed
- The INSTALL.md files in my Unit 6, 7, and 8 materials, for the voice guard, ship-gate, and PR monitor

