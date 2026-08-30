# Feature Report CSV Schema

**Launchify Feature Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| ID | Unique finding identifier (e.g., `FTR-001`) |
| Feature | Feature name |
| Category | Feature category (e.g., `authentication`, `payments`, `admin`) |
| Status | Current status (e.g., `active`, `deprecated`, `experimental`) |
| Classification | `COMPLETE`, `UNDERBUILT`, `OVERBUILT`, `PARTIALLY_IMPLEMENTED`, `BROKEN`, `INSECURE`, `UNRELIABLE`, `UNUSED`, `DUPLICATED`, `ABANDONED`, `MISSING_REQUIREMENTS`, `REVIEW_REQUIRED` |
| Confidence | `CONFIRMED`, `HIGH`, `MEDIUM`, `LOW` |
| Entry Points | User-facing entry points (routes, components, commands) |
| Files | Affected file paths |
| Services | Affected services or modules |
| Data Models | Affected database models or schemas |
| Evidence | Supporting evidence from code analysis |
| Missing Requirements | Production requirements that are absent |
| Security Concerns | Security issues identified in this feature |
| Reliability Concerns | Reliability issues identified in this feature |
| Complexity Concerns | Complexity issues identified in this feature |
| User Impact | Impact on end users |
| Business Impact | Impact on business objectives |
| Recommended Action | Recommended next step |
| Priority | `P0`, `P1`, `P2`, `P3` |
| Verification | How to verify the fix or change |

---

## Example Row

```
FTR-001,password-reset,authentication,active,UNDERBUILT,HIGH,/forgot-password,/src/pages/ForgotPassword.tsx,auth-service,User,Password reset sends email but does not expire tokens,"Missing token expiration, missing rate limiting, missing account lockout check",Tokens never expire — valid indefinitely,No rate limiting on reset endpoint,Users can request unlimited reset emails,Account takeover if email is compromised,Add token expiration, rate limiting, and lockout checks,P1,Run security regression tests for password reset flow
```
