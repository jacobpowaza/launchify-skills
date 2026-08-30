# Authorization and Access Control

**Category ID:** `authorization`

---

## Scope

Inspect all authorization checks, access control enforcement, tenant isolation, permission models, and privilege boundaries across the application. Authorization is the second door — authentication proves identity, authorization determines what that identity can access.

---

## Checks

### Missing Authorization
- Missing authorization checks on endpoints
- Broken access control (OWASP Top 10 #1)
- Unprotected admin routes (accessible without admin role)
- Exposed internal dashboards (admin panels, monitoring UIs)
- Hidden admin functionality accessible via direct URL
- Missing API authorization middleware
- Frontend-only security controls (authorization checks in JS only, not enforced server-side)
- Authorization checks applied after sensitive actions complete
- Authorization missing on background jobs
- Authorization missing on webhook handlers
- Authorization missing on scheduled tasks
- Authorization missing on file upload/download endpoints
- Authorization missing on search endpoints
- Authorization missing on export endpoints
- Authorization missing on bulk operation endpoints
- Authorization missing on versioning endpoints

### Object-Level Authorization (IDOR / BOLA)
- IDOR (Insecure Direct Object Reference) on user profiles
- IDOR on organization/team data
- IDOR on file downloads
- IDOR on API resources
- BOLA (Broken Object-Level Authorization) on any resource
- Cross-user access through predictable IDs
- Cross-user access through sequential IDs
- Cross-user access through UUID manipulation
- Missing ownership checks on resources
- Authorization bypass through alternate identifiers (email instead of ID)
- Authorization bypass through bulk operations (bulk endpoint missing per-item checks)
- Authorization bypass through export functionality
- Authorization bypass through background jobs (job runs with elevated privileges)
- Authorization bypass through webhook handlers
- Authorization bypass through cached responses (cache serves data to wrong user)
- Authorization bypass through GraphQL resolvers
- Authorization bypass through nested resource access
- Authorization bypass through API versioning
- Authorization bypass through pagination (accessing other users' pages)
- Authorization bypass through search (querying other users' data)

### Tenant Isolation
- Cross-tenant data access
- Poor tenant isolation in multi-tenant systems
- Missing tenant filters in database queries
- Missing row-level security where required
- Tenant ID manipulable through API
- Tenant isolation not enforced at database level
- Tenant isolation not enforced at API level
- Tenant isolation not enforced at cache level
- Tenant isolation not enforced at queue level
- Shared resources across tenants without isolation
- Missing tenant-aware logging
- Missing tenant-aware search indexing

### Permission Model
- Excessive permissions (user has more access than needed)
- Overprivileged roles (admin role given to non-admin functions)
- Mass assignment (user can set `role`, `admin`, `is_superuser` via API)
- Permission inheritance bugs (child resource inherits wrong permissions)
- Role escalation through parameter manipulation
- Role escalation through API endpoints
- Inconsistent authorization across API versions
- Confused-deputy behavior (service A authorized, acts on behalf of unauthorized user B)
- Missing service-to-service authorization
- Missing resource-level authorization
- Missing field-level authorization (user can read/write fields they shouldn't)
- Missing action-level authorization (user can perform actions they shouldn't)
- Missing namespace-level authorization
- Missing organization-level authorization
- Missing team-level authorization
- Role-based access control not enforced server-side
- Attribute-based access control not enforced
- Missing principle of least privilege
- Permissions not revoked when user role changes
- Permissions not revoked when user is deactivated
- Permissions not revoked when team membership changes

### Unprotected Admin Routes
- Admin dashboard accessible without authentication
- Admin API endpoints without admin authorization
- Admin user management without authorization
- Admin system configuration without authorization
- Admin billing/payment management without authorization
- Admin audit log access without authorization
- Admin feature flag management without authorization
- Admin deployment controls without authorization
- Admin database management without authorization
- Debug endpoints exposed in production
- Metrics endpoints exposed without authentication
- Health check endpoints leaking internal information
- GraphQL introspection enabled in production

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
14. Test mass assignment by including unexpected fields in request bodies
15. Test role escalation through API parameter manipulation
16. Verify cached responses respect authorization
17. Test search endpoints for cross-user data exposure

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Cross-tenant data access | CRITICAL |
| Missing authorization on admin route | CRITICAL |
| IDOR on sensitive user data | HIGH |
| Mass assignment allowing privilege escalation | HIGH |
| Frontend-only access control | HIGH |
| Authorization bypass through background job | HIGH |
| Authorization bypass through export | HIGH |
| Authorization bypass through cached response | MEDIUM |
| Missing resource-level authorization | MEDIUM |
| Missing field-level authorization | MEDIUM |

---

## Evidence Requirements

- Specific route or endpoint affected
- Required vs actual authorization level
- Steps to reproduce the bypass
- Whether tenant isolation is affected
- Impact on data confidentiality and integrity
- Whether the finding is in application code or infrastructure configuration
