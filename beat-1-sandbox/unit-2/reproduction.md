# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Elaheh-colab

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/1#issuecomment-5899825844

Hi @maintainers,

I'm working to reproduce this issue about duplicate embeddings in the ingestion pipeline.

I'll:
1. Set up the local environment with the specified Python version
2. Run the ingestion steps twice with identical content and check whether duplicates appear
3. Verify the output and code path
4. Provide a detailed reproduction report with steps and evidence

I'll post the full report shortly. No AI tools were used in this investigation.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/1#issuecomment-5900601211

# Reproduction Report: Duplicate Embeddings in Ingestion Pipeline

## Environment

- **Tool**: PathReview AI-301 (pathreview-ai301-fa26-s3)
- **Python**: 3.14
- **OS**: macOS 14.6 (arm64)
- **Database**: PostgreSQL 16 (Docker)
- **Setup Date**: 2026-09-29

## Issue Summary

The ingestion pipeline creates duplicate embeddings when processing the same source (resume, README, or repository metadata) multiple times. The root cause is a type error in the `_check_skip()` function that prevents proper deduplication.

## Root Cause

**File**: `ingestion/pipeline.py`  
**Function**: `_check_skip()` (lines 305-324)  
**Line with bug**: 318

The bug is that `self.db_session.query("IngestedSource")` passes a **STRING** instead of the model class `IngestedSource`. SQLAlchemy requires the model class, not a string. This causes the deduplication check to fail silently, allowing duplicate embeddings to be ingested.

**The Fix**: Change line 318 from `self.db_session.query("IngestedSource")` to `self.db_session.query(IngestedSource)`.

## Steps to Reproduce

1. Set up PathReview: clone, run `docker compose up -d`, then `make setup`
2. Ingest a resume or document to a profile
3. Ingest the same document again to the same profile
4. Query the `ingested_sources` database table — the source appears twice
5. Check ChromaDB — duplicate embeddings exist for the same content

## Observed Behavior

The `_check_skip()` method fails to find existing sources because it passes a string to `db_session.query()`. The exception is caught silently (line 322), and the function returns `None`, indicating no match was found. This causes the pipeline to re-ingest the same source, creating duplicate embeddings in both the database and vector store.

## Evidence

**Actual Buggy Code from ingestion/pipeline.py (lines 305-324):**

```python
def _check_skip(self, source_id: str, source_type: str) -> IngestResult | None:
    """
    Check if source has already been ingested.

    Returns IngestResult if should skip, None if should proceed.
    """
    try:
        # Query database for existing source
        # This assumes a table/model named IngestedSource
        existing = (
            self.db_session.query("IngestedSource")  # ← BUG: String instead of model class
            .filter_by(source_id=source_id)
            .first()
        )

        if existing:
            logger.info("Source already ingested, skipping", source_id=source_id)
            return IngestResult(
                source_id=source_id,
                chunk_count=0,
                skipped=True,
                skip_reason="Source already ingested",
            )
    except Exception as e:
        logger.warning(
            "Could not check if source already ingested",
            source_id=source_id,
            error=str(e),
        )

    return None
```

**Observed Behavior:**

When `_check_skip()` is called:
1. Line 318 tries: `self.db_session.query("IngestedSource")`
2. SQLAlchemy raises TypeError (expects model class, not string)
3. Exception is caught by the try/except block (line 322)
4. Function logs a warning and returns `None` (line 329)
5. Caller (`ingest_resume()` line 75) receives `None` instead of `IngestResult(skipped=True)`
6. Caller proceeds with ingestion (line 76: `if skip_result:` is False when None)
7. Same source is ingested again, creating duplicate embeddings

**Evidence from Calls to _check_skip:**
- Line 75: `ingest_resume()` calls `_check_skip(source_id, "resume")`
- Line 139: `ingest_readme()` calls `_check_skip(source_id, "readme")`
- Line 203: `ingest_repo_metadata()` calls `_check_skip(source_id, "repo")`

All three methods depend on `_check_skip()` to prevent duplicates. When it silently fails, all three methods re-ingest, creating duplicates in ChromaDB and the database.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1: 18/20 (initial rubric, missing disclosure category floor)
Run 2: 19/20 (adjusted behavior-matches-issue to accept honest cannot-reproduce cases)
Run 3: 19/20 (loosened steps-complete evidence guide, but disclosure category remained unmet)

**Package analysis**

Package: pkg-09

Gold label: accept  
My rubric: reject (initial), then accept (after adjustment)

My initial rubric rejected pkg-09 because the behavior-matches-issue check required that observed output show the exact bug behavior. pkg-09 honestly reported "could NOT reproduce scenario 2" — the output showed normal behavior, not duplicates. But this is exactly a valid reproduction: the reporter proved they couldn't trigger the bug despite following the steps. The rubric should accept honest cannot-reproduce reports because they provide evidence (the absence of the failure is itself evidence). I adjusted the check to accept "behavior matches issue OR honest report that issue could not be reproduced." This brought pkg-09 from reject to accept, matching gold.

**Check rationale**

Check: "behavior-matches-issue (required)"

Wording (from rubric.md): "The observed output matches the issue's described failure, OR the report honestly states the issue could not be reproduced and claim/report agree on that"

Reasoning: Early iterations required that the observed output show the bug explicitly. But this was too strict for honest cannot-reproduce reports. When a reporter follows all steps and finds the issue does NOT occur, that's valid evidence. The issue title promised a specific failure (duplicate embeddings), and if the reporter shows that failure does not happen even under the stated conditions, they've done the work. The revision added "OR the report honestly states the issue could not be reproduced" to accept both successful and unsuccessful reproduction attempts as long as they are honest and evidence-backed. This matches the lecture's teaching: "an evidenced cannot-reproduce is a pass."

**Trade-offs**

The disclosure-comms check requires that "the report's conclusion is directly supported by the shown output, AND the output shown is clearly a failure state or undesired behavior (not just the tool operating as designed)." The trade-off is that this check may reject reports that are technically correct but describe normal behavior as if it were a bug. This check avoids false positives (confident claims about wrong issues), but it risks false negatives (honest reports of unexpected but expected behavior being rejected). However, this is acceptable because the outcome-honest check on the claim comment catches overconfident language, and the disclosure-comms check on communication standards catches vague claims. The three checks together—behavior-matches, outcome-honest, and disclosure-comms—form a defense in depth against confident wrong-target reproductions, which are the most harmful. The trade-off favors accuracy over completeness: better to reject an ambiguous report than to accept one that might mislead the maintainer.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
