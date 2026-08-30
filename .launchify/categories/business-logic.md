# Business Logic Security

**Category ID:** `business-logic`

---

## Scope

Inspect all business logic for abuse vectors, workflow bypasses, and integrity violations.

---

## Checks

### Workflow Bypass
- Workflow bypasses
- Step skipping
- State machine manipulation
- Race conditions in business flows
- Incomplete state transitions
- Invalid state transitions accepted

### Data Integrity
- Business rule enforcement gaps
- Missing server-side validation for business rules
- Client-controlled business logic state
- Inconsistent business rule enforcement across endpoints
- Business logic that depends on client-provided order or sequence

### Abuse Prevention
- Missing abuse prevention controls
- Missing account sharing detection
- Missing usage monitoring
- Missing fraud detection
- Missing anomaly detection for business operations

### Entitlement Enforcement
- Missing entitlement enforcement
- Entitlement bypass through API manipulation
- Entitlement bypass through concurrent requests
- Stale entitlement cache
- Missing entitlement revocation

---

## Methodology

1. Map all business workflows and state machines
2. Test for workflow bypass by submitting invalid sequences
3. Test for race conditions in business flows
4. Verify business rules are enforced server-side
5. Test for entitlement bypass
6. Check for abuse prevention controls
7. Verify state machine transitions are properly validated
8. Test for concurrent request abuse
9. Check entitlement cache invalidation
10. Verify entitlement revocation works

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Workflow bypass allowing unauthorized access | CRITICAL |
| Race condition allowing duplicate entitlement | HIGH |
| Client-controlled business logic state | HIGH |
| Missing entitlement revocation | MEDIUM |
| Missing abuse prevention | MEDIUM |

---

## Evidence Requirements

- Business workflow affected
- Specific bypass vector
- Whether the finding allows unauthorized access or entitlement
- Impact on business integrity
