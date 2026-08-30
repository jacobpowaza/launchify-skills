# Feature Readiness

**Category ID:** `feature-readiness`

---

## Scope

Inspect all features for production readiness, completeness, security, reliability, and operational support.

---

## Checks

### Completeness
- Missing error handling
- Missing loading states
- Missing empty states
- Missing success states
- Missing edge case handling
- Incomplete user flows
- Missing confirmation dialogs for destructive actions
- Missing input validation
- Missing output validation

### Security
- Missing authorization on feature endpoints
- Missing tenant isolation for multi-tenant features
- Missing rate limiting on feature endpoints
- Missing input sanitization
- Missing CSRF protection
- Missing audit logging for feature actions

### Reliability
- Missing retry behavior
- Missing timeout handling
- Missing idempotency
- Missing rollback behavior
- Missing error recovery
- Missing graceful degradation
- Missing fallback behavior

### Operational Support
- Missing monitoring for feature usage
- Missing alerting for feature failures
- Missing metrics for feature health
- Missing documentation
- Missing admin or support workflows
- Missing feature-flag cleanup
- Missing deployment configuration
- Missing rollback configuration

### Accessibility
- Missing keyboard navigation
- Missing screen reader support
- Missing ARIA attributes
- Missing color contrast
- Missing focus management

### Testing
- Missing unit tests
- Missing integration tests
- Missing end-to-end tests
- Missing security regression tests
- Missing performance tests

---

## Methodology

1. Enumerate all features and their entry points
2. Test each feature for complete happy path and error paths
3. Verify authorization and tenant isolation
4. Check for retry, timeout, and idempotency
5. Verify monitoring and alerting
6. Check documentation completeness
7. Verify accessibility requirements
8. Check test coverage
9. Verify deployment and rollback configuration
10. Check admin and support workflows

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Missing authorization on feature endpoint | CRITICAL |
| Missing tenant isolation for multi-tenant feature | CRITICAL |
| Missing error handling on critical path | HIGH |
| Missing monitoring for feature | MEDIUM |
| Missing documentation | LOW |
| Missing accessibility support | MEDIUM |

---

## Evidence Requirements

- Feature affected
- Specific readiness gap
- Impact on users and operations
- Whether the gap affects security or reliability
