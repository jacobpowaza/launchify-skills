# API Security

**Category ID:** `api`

---

## Scope

Inspect all API endpoints, request/response handling, validation, rate limiting, authentication, authorization, and API-specific security controls. APIs are the primary attack surface for modern applications.

---

## Checks

### Authentication and Authorization
- Unsecured API endpoints (no authentication required)
- Missing API authentication middleware
- Missing API authorization checks
- Broken object-level authorization (BOLA)
- Unauthenticated health or diagnostic endpoints
- Unprotected metrics endpoints
- Unprotected administrative APIs
- API key authentication without rate limiting
- API keys not rotated
- API keys with excessive scope
- Missing API key revocation mechanism
- Bearer token not validated
- API authentication bypass through parameter pollution
- API authentication bypass through HTTP method switching
- API authentication bypass through content-type manipulation

### Input Validation
- Missing input validation on any endpoint
- Missing API schema validation (OpenAPI, JSON Schema)
- Unexpected fields accepted (mass assignment)
- Unexpected types accepted (string where integer expected)
- Missing request body size limits
- Missing array length limits
- Missing string length limits
- Missing number range validation
- Missing enum validation
- Missing boolean validation
- Missing date format validation
- Missing email format validation
- Missing URL format validation
- Missing nested object validation
- Missing file upload validation
- Unsafe file or URL parameters
- Unsafe webhook endpoints
- Missing validation on query parameters
- Missing validation on path parameters
- Missing validation on headers

### Data Exposure
- Excessive API data response (returning more than needed)
- Improper API response filtering
- Sensitive fields returned unnecessarily (password_hash, ssn, api_key)
- Hidden fields returned through alternate serializers
- Sensitive information in API error messages
- Stack traces in API error responses
- Internal service names in API errors
- Database queries in API error responses
- Version information leaked in API responses
- Internal IP addresses in API responses
- Full user objects returned when only name needed
- Sensitive data in API response headers
- GraphQL excessive data exposure through nested queries

### Rate Limiting and Quotas
- Missing rate limits on any endpoint
- Missing rate limiting on authentication endpoints
- Missing rate limiting on password reset
- Missing rate limiting on registration
- Missing rate limiting on file upload
- Missing throttling
- Missing quotas per user/key/IP
- Missing request-size limits
- Missing response-size limits
- Missing concurrency limits
- Missing timeouts on expensive operations
- Rate limit bypass through header manipulation
- Rate limit bypass through IP rotation
- Rate limit bypass through API key rotation
- Missing rate limiting on search endpoints
- Missing rate limiting on GraphQL queries

### API Abuse
- API enumeration (listing users, resources)
- API abuse automation (scraper, bot)
- Bots scraping expensive endpoints
- Missing idempotency keys on non-idempotent operations
- Duplicate request processing
- Missing replay protection
- API used for credential stuffing
- API used for account enumeration
- API used for data harvesting
- Missing API usage monitoring

### GraphQL Security
- GraphQL introspection enabled in production
- GraphQL query-depth attacks (nested queries)
- GraphQL query-complexity attacks (expensive operations)
- GraphQL excessive data exposure
- GraphQL resolver authorization failures
- GraphQL mutation authorization bypass
- GraphQL subscription information leakage
- GraphQL missing field-level authorization
- GraphQL batching attacks
- GraphQL denial-of-service through complex queries

### API Versioning and Legacy
- Old API versions remaining active
- Vulnerable legacy endpoints
- API version leakage
- Missing API deprecation process
- Missing API sunset headers
- Legacy endpoints with weaker security

### Gateway and Infrastructure
- Missing WAF protections
- Missing API gateway protections
- Missing centralized authentication
- Missing centralized rate limiting
- Missing centralized request validation
- Missing bot protection
- Missing DDoS protection
- Missing API schema enforcement
- Direct exposure of backend services
- Missing request-size limits at gateway
- Missing API version controls
- Gateway checks that fail open

### Consistency
- Inconsistent error handling across endpoints
- Missing API contract tests
- Broken pagination limits
- Downloading millions of records without limits
- Inconsistent response formats
- Missing API documentation
- Missing API health checks

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
11. Test for API enumeration
12. Test for credential stuffing through API
13. Verify API schema validation is enforced
14. Check API gateway configuration

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Unauthenticated API endpoint with sensitive data | CRITICAL |
| BOLA allowing cross-user data access | CRITICAL |
| Mass assignment allowing privilege escalation | HIGH |
| Missing rate limiting on authentication endpoint | HIGH |
| GraphQL introspection in production | MEDIUM |
| Excessive data in API response | MEDIUM |
| Missing API contract tests | LOW |
| API enumeration | MEDIUM |

---

## Evidence Requirements

- Specific endpoint or route affected
- HTTP method and request/response details
- Whether authentication/authorization is missing
- Whether input validation is bypassable
- Data sensitivity of exposed information
- Whether the endpoint is publicly accessible
