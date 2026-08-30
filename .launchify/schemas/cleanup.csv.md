# Cleanup Report CSV Schema

**Launchify Cleanup Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| ID | Unique finding identifier (e.g., `CLN-001`) |
| Type | `DEAD_CODE`, `DUPLICATE_LOGIC`, `UNUSED_COMPONENT`, `UNNECESSARY_COMPLEXITY`, `AI_DEBRIS`, `DEPENDENCY`, `CONFIGURATION`, `ARCHITECTURE`, `INCOMPLETE_REFACTOR`, `TEST`, `DOCUMENTATION` |
| Confidence | `CONFIRMED`, `HIGH`, `MEDIUM`, `LOW` |
| File | Affected file path |
| Location | Line number or range |
| Finding | Brief description of the cleanup finding |
| Evidence | Supporting evidence |
| Current Purpose | What the code/config currently does (or appears to do) |
| Recommended Action | `SAFE_TO_REMOVE`, `SAFE_TO_SIMPLIFY`, `REVIEW_REQUIRED`, `LIKELY_INTENTIONAL`, `DO_NOT_TOUCH` |
| Risk | `NONE`, `LOW`, `MEDIUM`, `HIGH` |
| Files Affected | Number of files that would be affected by this change |
| Status | `OPEN`, `FIXED`, `WONT_FIX`, `DEFERRED` |
| Verification | How to verify the cleanup was safe |

---

## Example Row

```
CLN-001,DEAD_CODE,CONFIRMED,src/utils/old-api.ts,1-45,Unused API client for deprecated v1 endpoint,"No imports found, no runtime registration, API version removed in v2",Previously used for v1 API calls,SAFE_TO_REMOVE,NONE,1,FIXED,Run tests and verify no import errors
```
