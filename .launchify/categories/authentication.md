# Authentication and Identity Security

**Category ID:** `authentication`

---

## Scope

Inspect all authentication mechanisms, identity management, session handling, token management, OAuth/SSO flows, MFA, password management, and identity-provider integrations. Authentication is the front door — if it is broken, everything behind it is exposed.

---

## Checks

### Password Security
- Weak password policies (no minimum length, no complexity requirements)
- Passwords stored in plaintext or reversibly encrypted
- Passwords hashed with weak algorithms (MD5, SHA1, unsalted SHA256)
- Missing password complexity requirements
- Missing account lockout after failed attempts
- Missing rate limiting on login endpoints
- Password visible in URL parameters
- Password transmitted over unencrypted connection
- Password logged in application logs
- Password reset tokens that do not expire
- Password reset tokens reusable after use
- Password reset tokens predictable or guessable
- Password reset flow allows account enumeration
- Password reset flow leaks whether email exists
- Password reset via insecure channel (SMS without app backup)
- Password history not enforced (user can reuse old passwords)

### Broken Password Reset
- Password reset token in URL (logged by proxies, browsers, analytics)
- Password reset token sent over unencrypted channel
- Password reset token not single-use
- Password reset token has long expiration (>1 hour)
- Password reset flow does not verify identity before reset
- Password reset allows setting new password without current password
- Password reset response reveals whether email is registered
- Password reset link sent to compromised email without additional verification

### Session Management
- Session fixation (attacker sets session ID before login)
- Session IDs predictable or sequential
- Session tokens not rotated after login
- Session tokens not rotated after privilege change
- Session tokens not rotated after password change
- Missing session expiration (sessions live forever)
- Missing session idle timeout
- Missing session absolute timeout
- Session token in URL (logged by proxies, browsers)
- Session token in localStorage (accessible to XSS)
- Session token in cookie without HttpOnly flag
- Session token in cookie without Secure flag
- Session token in cookie without SameSite attribute
- Session not invalidated on logout
- Session not invalidated on password change
- Session not invalidated on account deletion
- Missing concurrent session control
- Missing device/session tracking
- Missing session revocation mechanism
- Missing admin session revocation capability
- Session token in response body (leaked through Referer header)

### JWT Security
- JWT secret hardcoded in source code
- JWT secret in environment variable without rotation
- JWT using `alg: none` (bypasses signature verification)
- JWT using weak signing algorithm (HS256 with weak secret)
- JWT algorithm confusion (RS256→HS256 attack)
- JWT not validated on protected endpoints
- JWT audience not validated
- JWT issuer not validated
- JWT expiration not validated
- JWT not revoked on logout
- JWT not revoked on password change
- JWT stored in localStorage (accessible to XSS)
- JWT stored in cookie without HttpOnly
- JWT with no expiration (immortal tokens)
- JWT with excessive expiration (>30 days)
- JWT secret smaller than 256 bits
- JWT secret not unique per environment
- JWT contains sensitive data in payload (passwords, PII)
- JWT signing key exposed through JWKS endpoint without restriction

### OAuth / SSO Security
- Missing OAuth state parameter (CSRF on OAuth callback)
- Missing PKCE (Proof Key for Code Exchange)
- OAuth state parameter not validated
- OAuth state parameter predictable
- OAuth redirect URI not validated (open redirect)
- OAuth redirect URI allows wildcards
- OAuth token leakage through Referer header
- OAuth token leakage through browser history
- OAuth token leakage through referrer from redirect
- OAuth tokens stored in insecure storage
- OAuth token exchange over HTTP instead of HTTPS
- OAuth token with excessive scopes
- OAuth refresh token not rotated
- OAuth refresh token with infinite lifetime
- OAuth callback does not verify token before establishing session
- OAuth provider not validating email verification
- OAuth account linking allows account takeover
- Missing PKCE for public clients (SPAs, mobile apps)
- SAML assertion not signed
- SAML assertion signature not validated
- SAML response not validated against recipient
- SAML response replay possible
- SAML NameID not encrypted

### MFA Security
- Missing MFA on sensitive accounts
- MFA bypassable through API
- MFA bypassable through backup codes without rate limiting
- MFA backup codes not single-use
- MFA recovery allows bypass without additional verification
- TOTP secret shared across users
- MFA enforcement not applied to admin accounts
- MFA enforcement not applied to service accounts
- MFA tokens valid for too long
- Missing MFA for privileged operations (password change, email change, etc.)

### Privilege Escalation
- User-to-admin escalation through API parameter manipulation
- User-to-admin escalation through role field in registration
- User-to-admin escalation through profile update endpoint
- Role confusion (frontend thinks user is admin but backend disagrees)
- Missing server-side role enforcement
- Authorization checks applied after sensitive actions
- Authentication bypass through alternate endpoints
- Authentication bypass through HTTP method manipulation
- Authentication bypass through case sensitivity tricks
- Authentication checks applied only in the frontend
- Inconsistent identity handling across services
- Missing identity-provider validation
- Account takeover through email change without verification
- Account takeover through password reset with weak verification

### Account Recovery
- Weak security questions (guessable answers)
- Account recovery via email without additional verification
- Account recovery flow allows account enumeration
- Account recovery tokens not expired after use
- Account recovery flow does not log recovery attempts
- Account recovery does not invalidate existing sessions
- Account recovery does not notify the account owner
- Backup codes not stored securely
- Backup codes predictable

---

## Methodology

1. Trace all authentication flows end-to-end (registration, login, logout, reset, MFA)
2. Inspect session token generation, storage, transmission, and expiration
3. Inspect JWT signing, validation, algorithm selection, and secret management
4. Inspect OAuth/SSO configuration for state, PKCE, redirect validation, scope minimization
5. Test for authentication bypass through alternate endpoints, HTTP methods, or parameter manipulation
6. Verify authentication is enforced server-side, not just in the frontend
7. Check for account enumeration through error messages, timing, or response differences
8. Verify session revocation works (logout, password change, admin action)
9. Check for missing MFA support where required
10. Inspect identity-provider integrations for validation and trust boundaries
11. Test privilege escalation through role manipulation
12. Test password reset flow for token security and enumeration
13. Verify password hashing uses modern algorithms (bcrypt, scrypt, Argon2)
14. Check for concurrent session management

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Authentication bypass | CRITICAL |
| JWT algorithm confusion allowing bypass | CRITICAL |
| User-to-admin privilege escalation | CRITICAL |
| Session fixation | HIGH |
| Missing PKCE in OAuth | HIGH |
| Password reset token in URL | HIGH |
| JWT secret hardcoded in source | HIGH |
| Missing MFA on admin accounts | HIGH |
| Session not invalidated on logout | MEDIUM |
| Account enumeration | MEDIUM |
| Weak password policy | MEDIUM |
| JWT with no expiration | MEDIUM |

---

## Evidence Requirements

- Authentication flow being tested
- Specific bypass vector or weakness
- Affected endpoints
- Whether the finding is code-level or configuration-level
- Whether runtime validation is needed to confirm
- Impact on account security and data access
