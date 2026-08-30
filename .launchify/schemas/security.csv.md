# Security Report CSV Schema

**Launchify Security Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| ID | Unique finding identifier (e.g., `SEC-001`) |
| Category | Security category (canonical name from spec) |
| Severity | `CRITICAL`, `HIGH`, `MEDIUM`, `LOW`, `INFO` |
| Confidence | `CONFIRMED`, `HIGH`, `MEDIUM`, `LOW`, `NEEDS_RUNTIME_VALIDATION`, `NEEDS_PRODUCT_CLARIFICATION` |
| File | Affected file path |
| Location | Line number or range (e.g., `42`, `42-58`) |
| Component | Affected component or module |
| Feature | Affected feature or user-facing flow |
| Infrastructure Resource | Affected infrastructure resource (if applicable) |
| Issue | Brief description of the vulnerability or issue |
| Evidence | Supporting evidence from code, configuration, or infrastructure |
| Attack Prerequisites | What an attacker needs to exploit this |
| Exploit Path | How the vulnerability is exploited |
| Impact | Business and technical impact |
| Recommendation | Recommended remediation action |
| Status | `OPEN`, `FIXED`, `WONT_FIX`, `FALSE_POSITIVE`, `DEFERRED` |
| Verification | How to verify the fix |
| Runtime Validation Required | `YES` or `NO` — whether cloud/runtime access is needed to confirm |

---

## Example Row

```
SEC-001,secrets,CRITICAL,CONFIRMED,.env,1,environment,configuration,N/A,Hardcoded database password in .env file,"Password 'supersecret123' found in plain text",Attacker gains read access to repository,Read .env file,Full database access including all user data,Move secrets to secret manager and rotate credentials,FIXED,Verify .env is in .gitignore and secrets are in secret manager,NO
```
