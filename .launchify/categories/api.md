# API Security

**Category ID:** `api`

---

## Scope

Inspect all API endpoints, request/response handling, validation, rate limiting, and API-specific security controls.

---

## Checks

### Authentication and Authorization
- Unsecured API endpoints
- Missing API authentication
- Missing API authorization
- Broken object-level authorization
- Unauthenticated health or diagnostic endpoints
- Unprotected metrics endpoints
- Unprotected administrative APIs

### Input Validation
- Missing input validation
- Missing API schema validation
- Unexpected fields accepted
- Unexpected types accepted
- Mass assignment through request bodies
- Unsafe file or URL parameters
- Unsafe webhook endpoints

### Data Exposure
- Excessive API data exposure
- Improper API response filtering
- Sensitive fields returned unnecessarily
- Hidden fields returned through alternate serializers
- Sensitive information in API errors

### Rate Limiting and Quotas
- Missing rate limits
- Missing throttling
- Missing quotas
- Missing timeouts
- Missing request-size limits
- Missing response-size limits
- Missing concurrency limits

### API Abuse
- API enumeration
- API abuse automation
- Bots scraping expensive endpoints
- Missing idempotency keys
- Duplicate request processing
- Missing replay protection

### GraphQL
- GraphQL vulnerabilities
- GraphQL introspection exposure
- GraphQL query-depth attacks
- GraphQL query-complexity attacks
- GraphQL excessive data exposure
- GraphQL resolver authorization failures

### API Versioning
- Old API versions remaining active
- Vulnerable legacy endpoints
- API version leakage
- Missing gateway protections
- Missing WAF protections

### Consistency
- Inconsistent error handling
- Missing API contract tests
- Broken pagination limits
- Downloading millions of records

---

## Methodology

1. Enumerate all API endpoints and their authentication requirements
2. Test each endpoint for authorization enforcement
3. Test input validation by sending unexpected types, sizes, and values
4. Test for mass assignment by including unexpected fields in request bodies
5. Check response filtering for excessive data exposure
6. Test rate limiting and throttling behavior
7. Test GraphQL endpoints for introspection, depth, and complexity attacks
8. Test old API versions for vulnerabilities
9. Verify API contract tests exist and are meaningful
10. Check for idempotency on non-idempotent operations

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Unauthenticated API endpoint with sensitive data | CRITICAL |
| Mass assignment allowing privilege escalation | HIGH |
| Missing rate limiting on authentication endpoint | HIGH |
| GraphQL introspection in production | MEDIUM |
| Excessive data in API response | MEDIUM |
| Missing API contract tests | LOW |

---

## Evidence Requirements

- Specific endpoint or route affected
- HTTP method and request/response details
- Whether authentication/authorization is missing
- Whether input validation is bypassable
- Data sensitivity of exposed information
