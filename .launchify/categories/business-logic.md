# Business Logic Security

**Category ID:** `business-logic`

---

## Scope

Inspect all business logic for abuse vectors, workflow bypasses, state machine manipulation, and integrity violations. Business logic bugs don't show up in security scanners — they require business context to identify.

---

## Checks

### Workflow Bypass
- Workflow bypasses (skipping steps in multi-step flows)
- Step skipping (completing a flow without required intermediate steps)
- State machine manipulation (forcing invalid state transitions)
- Race conditions in business flows
- Incomplete state transitions
- Invalid state transitions accepted
- Missing state validation
- Missing transition guards
- Missing state machine documentation
- Workflow order manipulation

### Time-of-Check/Time-of-Use (TOCTOU)
- TOCTOU in file operations
- TOCTOU in balance/credit checks
- Race condition in inventory management (overselling)
- Race condition in limit enforcement (overdraft)
- Missing distributed locking on shared resources
- Optimistic locking not implemented where needed
- TOCTOU in permission checks
- TOCTOU in resource availability checks

### Data Integrity
- Business rule enforcement gaps
- Missing server-side validation for business rules
- Client-controlled business logic state
- Inconsistent business rule enforcement across endpoints
- Business logic that depends on client-provided order or sequence
- Missing input validation for business rules
- Missing output validation for business decisions
- Inconsistent behavior across API versions
- Missing audit trail for business decisions

### Abuse Prevention
- Missing abuse prevention controls
- Missing account sharing detection
- Missing usage monitoring
- Missing fraud detection
- Missing anomaly detection for business operations
- Missing rate limiting on business operations
- Missing abuse reporting
- Missing IP-based abuse detection
- Missing device-based abuse detection
- Missing behavioral analysis

### Entitlement Enforcement
- Missing entitlement enforcement
- Entitlement bypass through API manipulation
- Entitlement bypass through concurrent requests
- Stale entitlement cache
- Missing entitlement revocation
- Entitlement not checked on all access paths
- Entitlement checked client-side only
- Missing entitlement audit logging
- Entitlement propagation failures across services

### Account and User Abuse
- Account creation abuse (mass account creation)
- Account takeover through business logic
- Account sharing detection
- Identity verification bypass
- KYC (Know Your Customer) bypass
- Missing age verification where required
- Missing geographic restrictions where required

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
11. Test for business logic that depends on client-provided values
12. Verify audit trail for business decisions
13. Test for inconsistent behavior across endpoints

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Workflow bypass allowing unauthorized access | CRITICAL |
| Race condition allowing duplicate entitlement | HIGH |
| Client-controlled business logic state | HIGH |
| Missing entitlement enforcement | HIGH |
| Entitlement bypass through API manipulation | HIGH |
| Missing abuse prevention | MEDIUM |
| Missing entitlement revocation | MEDIUM |
| Stale entitlement cache | MEDIUM |

---

## Evidence Requirements

- Business workflow affected
- Specific bypass vector
- Whether the finding allows unauthorized access or entitlement
- Impact on business integrity
- Whether the finding allows financial loss
