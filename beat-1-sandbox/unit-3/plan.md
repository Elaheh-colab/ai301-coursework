# Unit 3 — Plan and Build: Duplicate Embeddings Fix

## Diagnosis

The ingestion pipeline creates duplicate embeddings when processing the same source multiple times because the deduplication check in `_check_skip()` fails silently.

**Root cause**: In `ingestion/pipeline.py` line 318, the code passes a **string** `"IngestedSource"` to `db_session.query()` instead of the model class `IngestedSource`. SQLAlchemy requires the model class, not a string. When the string is passed, SQLAlchemy raises a `TypeError`, which is caught by the try/except block (line 322), causing the function to return `None` instead of `IngestResult(skipped=True)`.

**Evidence from reproduction report**:
- The buggy code (lines 305-324):
```python
def _check_skip(self, source_id: str, source_type: str) -> IngestResult | None:
    try:
        existing = (
            self.db_session.query("IngestedSource")  # ← BUG: String instead of model class
            .filter_by(source_id=source_id)
            .first()
        )
        if existing:
            logger.info("Source already ingested, skipping", source_id=source_id)
            return IngestResult(skipped=True, ...)
    except Exception as e:
        logger.warning("Could not check if source already ingested", ...)
    return None
```

- When `_check_skip()` returns `None` instead of `IngestResult(skipped=True)`, the callers (`ingest_resume()` at line 75, `ingest_readme()` at line 139, `ingest_repo_metadata()` at line 203) proceed with ingestion, creating duplicates in both the database and ChromaDB vector store.

- **Observed behavior** (from repro): ingest same content twice → query database → source appears twice → check ChromaDB → duplicate embeddings exist. This matches the issue.

## Scope

**In scope**: One line change in `ingestion/pipeline.py` line 318.

**Out of scope**: Any changes to the syntax highlighting pipeline, error handling beyond the immediate fix, or other deduplication mechanisms.

**Files to change**:
- `ingestion/pipeline.py` — line 318 only

## Approach

1. Change line 318 from:
   ```python
   self.db_session.query("IngestedSource")
   ```
   to:
   ```python
   self.db_session.query(IngestedSource)
   ```
   (Remove the quotes around `IngestedSource` to pass the model class instead of a string.)

2. No other changes needed; the rest of the function logic is correct.

3. All three callers of `_check_skip()` will automatically benefit: `ingest_resume()`, `ingest_readme()`, `ingest_repo_metadata()`.

## Test plan

**Re-run Unit 2 repro steps** (from reproduction report):

1. Set up PathReview: clone, run `docker compose up -d`, then `make setup`
2. Ingest a resume or document to a profile
3. Ingest the **same document again** to the same profile
4. Query the `ingested_sources` database table — verify the source appears **only once** (not twice)
5. Check ChromaDB — verify **no duplicate embeddings** exist for the same content
6. Expected: After the fix, step 3's ingestion is skipped (logged as "Source already ingested"), and step 4 shows only one entry in the database.

**Also verify**: The three callers all still work correctly:
- `ingest_resume()` skips on duplicate
- `ingest_readme()` skips on duplicate
- `ingest_repo_metadata()` skips on duplicate

## Risks and unknowns

**Risk**: None identified. This is a one-line fix that removes the type error. The logic downstream is already correct and waits for the fix to work.

**Unknown**: Whether there are other similar string-instead-of-class bugs elsewhere in the codebase. The fix addresses the specific issue in `_check_skip()`, and a broader search for similar patterns could be a follow-up.

## Deviations

**Minor implementation details, no change to the fix itself:**

1. **Actual line number**: The repro notes referenced line 318, but the actual buggy code was at line 298 in the current codebase. Changed the correct line (298) instead.

2. **Added import**: Had to add `from .core.models.ingested_source import IngestedSource` to the imports since the model class was not imported. This was necessary to make the fix work — SQLAlchemy needs access to the actual class, not just the name.

**Result**: The fix is identical to the plan — pass the model class instead of a string to `query()`. The deduplication check in `_check_skip()` now works correctly across all three ingestion methods.
