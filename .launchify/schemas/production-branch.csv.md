# Production Branch Report CSV Schema

**Launchify Production Branch Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| Change ID | Unique identifier for the change (e.g., `CHG-001`) |
| Type | Change type (feature, page, component, endpoint, model, migration, config, infrastructure, dependency, refactor, fix, security, test, documentation, cleanup) |
| Files | Affected files (semicolon-separated) |
| Feature | Feature name (if applicable) |
| Classification | MERGE_READY, MERGE_WITH_CAUTION, NEEDS_FIXES, NEEDS_REVIEW, HOLD, DEV_ONLY, REVERT |
| Risk | NONE, LOW, MEDIUM, HIGH, CRITICAL |
| Security | Security assessment summary |
| Reliability | Reliability assessment summary |
| Testing | Test coverage assessment |
| Data Integrity | Migration/data assessment |
| Deployment | Deployment requirements |
| Documentation | Documentation status |
| Blockers | Specific issues blocking merge |
| Recommendation | Recommended action |

---

## Example Row

```
CHG-001,endpoint,src/routes/auth.ts;src/controllers/auth.ts,authentication,NEEDS_FIXES,HIGH,Missing rate limiting on login endpoint;Missing account lockout;Tests present but no security regression tests,No retry or timeout handling,Unit tests present but integration tests missing,No migration,Requires environment variable for JWT secret,README updated,Rate limiting must be added before merge,Add rate limiting and account lockout
```
