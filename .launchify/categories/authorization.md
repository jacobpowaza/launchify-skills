# Authorization and Access Control

**Category ID:** `authorization`

---

## Scope

Inspect all authorization checks, access control enforcement, tenant isolation, permission models, and privilege boundaries across the application.

---

## Checks

### Missing Authorization
- Missing authorization checks
- Broken access control
- Unprotected admin routes
- Exposed internal dashboards
- Hidden admin functionality
- Missing API authorization
- Frontend-only security controls
- Authorization checks applied after sensitive actions

### Object-Level Authorization
- IDOR (Insecure Direct Object Reference)
- BOLA (Broken Object-Level Authorization)
- Cross-user access
- Cross-tenant access
- Poor tenant isolation
- Missing ownership checks
- Authorization bypass through alternate identifiers
- Authorization bypass through bulk operations
- Authorization bypass through exports
- Authorization bypass through background jobs
- Authorization bypass through webhooks
- Authorization bypass through cached responses

### Permission Model
- Excessive permissions
- Overprivileged roles
- Mass assignment
- Permission inheritance bugs
- Role escalation
- Inconsistent authorization across API versions
- Confused-deputy behavior
- Missing service-to-service authorization
- Missing resource-level authorization
- Missing field-level authorization

---

## Methodology

1. Enumerate all routes, endpoints, and API surfaces
2. For each route, identify the required authorization level
3. Trace the authorization check in the code
4. Test whether changing resource IDs crosses security boundaries
5. Test whether unauthenticated or low-privilege users can access high-privilege resources
6. Test for IDOR/BOLA by substituting resource identifiers
7. Test admin routes for proper authorization enforcement
8. Test background jobs and webhooks for authorization bypass
9. Verify tenant isolation in multi-tenant systems
10. Verify field-level authorization for sensitive data
11. Test bulk operations for authorization bypass
12. Test export functionality for authorization bypass
13. Verify authorization is enforced server-side, not just in the frontend

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| IDOR on user profile data | HIGH |
| Cross-tenant data access | CRITICAL |
| Missing authorization on admin route | CRITICAL |
| Mass assignment allowing privilege escalation | HIGH |
| Frontend-only access control | HIGH |
| Authorization bypass through background job | HIGH |

---

## Evidence Requirements

- Specific route or endpoint affected
- Required vs actual authorization level
- Steps to reproduce the bypass
- Whether tenant isolation is affected
- Impact on data confidentiality and integrity
