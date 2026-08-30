# Frontend Security

**Category ID:** `frontend`

---

## Scope

Inspect all client-side security controls, frontend-specific vulnerabilities, browser storage, third-party script risks, and client-side authorization enforcement.

---

## Checks

### Client-Side Security Reliance
- Client-side security reliance
- Frontend-only authorization bypass
- Hidden UI used as security
- Disabled buttons bypassed through direct API calls
- Client-side payment checks
- Client-controlled entitlement state
- Client-controlled prices, product identifiers, discounts, subscription status

### Secrets and Sensitive Data
- Frontend secrets
- Firebase keys or tokens exposed inappropriately
- API tokens exposed in bundles
- Exposed source maps
- Unsafe localStorage usage
- Sensitive browser storage
- Sensitive data in sessionStorage or IndexedDB
- Tokens accessible to unnecessary scripts
- Sensitive cached data
- Source-code and environment leakage

### Third-Party Script Risks
- Third-party script risks
- Analytics risks
- Chat-widget risks
- CDN script risks
- Untrusted CDN dependencies
- Missing Subresource Integrity where appropriate

### DOM Security
- DOM-based XSS
- Prototype pollution
- Unsafe HTML rendering
- Unsafe markdown rendering
- Unsafe URL handling
- Insecure postMessage usage
- Insecure service workers
- Cache leakage

### Browser Security
- Missing clickjacking protection
- Exposed feature flags
- Debug tooling exposed in production

---

## Methodology

1. Search frontend bundles for embedded secrets, API keys, tokens
2. Verify source maps are not publicly accessible
3. Test for client-side authorization bypass (disabled buttons, hidden elements)
4. Inspect browser storage for sensitive data
5. Audit third-party scripts for risks and Subresource Integrity
6. Test DOM-based XSS vectors
7. Test postMessage handling for origin validation
8. Verify CSP is configured to restrict script execution
9. Check for exposed feature flags in client code
10. Verify debug tooling is disabled in production builds

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| API key in frontend bundle | CRITICAL |
| Client-side payment validation only | HIGH |
| Sensitive data in localStorage | HIGH |
| Exposed source maps in production | MEDIUM |
| Missing Subresource Integrity | MEDIUM |
| Debug tooling in production | LOW |

---

## Evidence Requirements

- Specific frontend file or component affected
- Whether the secret or sensitive data is accessible to all users
- Whether client-side checks can be bypassed via direct API calls
- Browser storage location of sensitive data
