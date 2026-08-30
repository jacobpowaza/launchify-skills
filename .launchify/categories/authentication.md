# Authentication and Identity Security

**Category ID:** `authentication`

---

## Scope

Inspect all authentication mechanisms, identity management, session handling, token management, OAuth/SSO flows, and identity-provider integrations.

---

## Checks

### Password Security
- Weak authentication mechanisms
- Weak password policies
- Broken password reset flows
- Password reset token leakage
- Weak recovery questions
- Unsafe email-change workflows
- Missing identity verification

### Session Management
- Session fixation
- Weak session management
- Session theft protection missing
- Missing device or session tracking
- Missing session revocation
- Missing session expiration

### Token Security
- JWT secret exposure
- Weak JWT signing algorithms
- JWT validation bypass
- JWT algorithm confusion
- Token audience or issuer validation failures

### OAuth/SSO
- OAuth misconfiguration
- Missing OAuth state parameter
- Missing PKCE
- OAuth token leakage
- OAuth token over-permissioning
- Unnecessary OAuth scopes
- Broken SSO
- Broken callback validation
- Open redirect in OAuth flows

### Privilege Escalation
- Privilege escalation paths
- Role confusion
- User-to-admin escalation through API manipulation
- Missing identity-provider validation
- Authentication bypass through alternate endpoints
- Authentication checks applied only in the frontend
- Inconsistent identity handling across services

---

## Methodology

1. Trace all authentication flows end-to-end (registration, login, reset, MFA)
2. Inspect session token generation, storage, transmission, and expiration
3. Inspect JWT signing, validation, algorithm selection, and secret management
4. Inspect OAuth/SSO configuration for state, PKCE, redirect validation, scope minimization
5. Test for authentication bypass through alternate endpoints, HTTP methods, or parameter manipulation
6. Verify authentication is enforced server-side, not just in the frontend
7. Check for account enumeration through error messages, timing, or response differences
8. Verify session revocation works (logout, password change, admin action)
9. Check for missing MFA support where required
10. Inspect identity-provider integrations for validation and trust boundaries

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Authentication bypass | CRITICAL |
| JWT algorithm confusion | CRITICAL |
| Missing PKCE in OAuth | HIGH |
| Session fixation | HIGH |
| Weak password policy | MEDIUM |
| Account enumeration | MEDIUM |
| Missing MFA (where expected) | MEDIUM |

---

## Evidence Requirements

- Authentication flow being tested
- Specific bypass vector or weakness
- Affected endpoints
- Whether the finding is code-level or configuration-level
- Whether runtime validation is needed to confirm
