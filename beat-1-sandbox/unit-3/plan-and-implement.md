# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Elaheh-colab

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/1#issuecomment-6112710104

I reproduced this issue on the current version (report in unit 2 work). The root cause is a type error in `_check_skip()` at line 318: passing a string `"IngestedSource"` instead of the model class `IngestedSource` to `db_session.query()`. SQLAlchemy raises a `TypeError`, which the try/except silently catches, causing the function to return `None` instead of skipping the duplicate.

My plan: fix line 318 to pass the model class without quotes. This single-line change restores the deduplication check across all three ingestion methods. I'll verify with the repro steps: ingest the same content twice and confirm the database and ChromaDB show no duplicates.

---

## Your branch

**Branch**

fix/1-string-to-class

**Evidence**

Command:
```bash
cd ~/Desktop/Codepath-ai301/unit1/pathreview-ai301-fa26-s3 && source .venv/bin/activate && python3 test_fix_verification.py
```

Before fix (buggy code with string query):
```
TEST 2a: BUGGY CODE - Query with string 'IngestedSource'
✓ EXPECTED ERROR: ArgumentError: Textual column expression 'IngestedSource' 
  should be explicitly declared with text('IngestedSource')...
This is what happens in the buggy code - exception is caught and ignored
Result: Exception caught, returns None → Duplicate allowed ✗
```

After fix (fixed code with class query):
```
TEST 2b: FIXED CODE - Query with class IngestedSource
✓ FOUND: resume_123 (source_type: resume)
  Result type: IngestedSource instance
  Query would return IngestResult(skipped=True) - DUPLICATE PREVENTED

TEST 3: FULL FLOW - Simulate ingest_resume() with fix
Step 1: First ingest of resume_123
  → check_skip() returned None: PROCEED with ingestion
Step 2: Second ingest of SAME resume_123 (should be skipped)
  → ✓ CORRECT: Source resume_123 already ingested
  → Ingestion SKIPPED - no duplicates created
Step 3: Ingest different source (should proceed)
  → ✓ CORRECT: check_skip() returned None: PROCEED with ingestion

SUMMARY:
BEFORE FIX: query('IngestedSource') raises error, caught silently, returns None → Duplicates created ✗
AFTER FIX: query(IngestedSource) works, finds source, prevents duplicates ✓
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1: 17/20 (initial rubric with diagnosis, scope, test-plan checks only; missing thread-convention category)
Run 2: 19/20 (added comms check to rubric; fixed pkg-04 and pkg-14; thread-convention now 1/2)
Run 3: 20/20 (refined comms check to require explicit AI disclosure when repo policy requires it and AI is mentioned in thread; fixed pkg-20)

**Package analysis**

Package: pkg-04 (thread-convention category)

My rubric: reject (comms check fails)
Gold label: reject

Why my rubric reads it that way: The thread highlights show the maintainer (junegunn) identified the specific code location causing the bug ("the console input handling in `src/tui/light_windows.go` (lines 70-84)"). However, the candidate plan proposes a documentation-only fix without any code changes and explicitly states "Not in scope: any change to fzf's input handling code." My comms check requires that the plan comment respond to maintainer guidance in the thread. The plan ignores the maintainer's diagnostic direction and proposes a different approach (documentation instead of code fix), so it fails the comms check.

**Check rationale**

From rubric.md:

"comms (required) | The plan comment read against thread highlights and repo-facts AI policy | The plan comment responds to maintainer guidance in the thread (if any); if the repo requires AI disclosure AND AI is mentioned in the thread, the comment explicitly addresses the AI aspect (either disclosing use or clarifying the plan is not AI-assisted) | required"

This check reads this way because I revised it during eval to catch two failure modes: (1) plans that ignore maintainer diagnostic guidance shown in the thread, and (2) plans that hide required AI disclosure when AI is discussed in the thread. Initially, my comms check only required responding to maintainers; I refined it to explicitly require addressing the AI aspect when the repo has strict AI policy and AI is mentioned in thread highlights. This catches cases like pkg-20 where the plan discusses an AI proposal from the thread but never discloses whether the plan author used AI assistance.

**Trade-offs**

The comms check gives up the ability to grade plans where the thread is ambiguous about whether maintainer guidance is a strict requirement or just one option. The check assumes that if a maintainer names a diagnosis or direction in thread highlights, the plan should engage with it (either adopt, adapt, or explicitly explain why not). This rejects plans that diverge from thread signals without acknowledgment. However, in rare cases this could reject a plan that independently arrived at a better approach that the maintainer didn't consider. The trade-off accepts false positives (rejecting some good plans) to catch false negatives (accepting plans that ignore important thread signals). Also, the requirement for explicit AI disclosure when AI is mentioned in the thread is strict—it assumes any plan discussing an AI-proposed solution must clarify whether the author used AI. This could penalize plans that reference AI proposals purely for context without using them, but the trade-off favors honesty and transparency when AI is part of the conversation.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
