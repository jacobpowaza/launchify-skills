# Frontend Security

**Category ID:** `frontend`

---

## Scope

Inspect all client-side security controls, frontend-specific vulnerabilities, browser storage, third-party script risks, client-side authorization enforcement, and secrets exposure in frontend code. Frontend code runs in the user's browser — anything in it is accessible to attackers.

---

## Checks

### Client-Side Security Reliance
- Client-side authorization bypass (disabled buttons, hidden elements, CSS display:none)
- Frontend-only authorization checks (no server-side enforcement)
- Hidden UI elements used as security controls
- Disabled buttons bypassed through direct API calls
- Client-side payment validation only (no server-side verification)
- Client-controlled entitlement state
- Client-controlled prices, product identifiers, discounts
- Client-controlled subscription status
- Client-controlled feature flags affecting security
- Client-controlled role or permission fields
- JavaScript validation without server-side validation
- Hidden form fields with sensitive values
- Client-side encryption without server-side validation
- Client-side rate limiting only

### Secrets and Sensitive Data in Frontend
- API keys in frontend JavaScript bundles
- Firebase API keys exposed inappropriately
- Firebase config containing sensitive values
- AWS Amplify configuration with access keys
- Google Maps API keys (low risk but enumerable)
- Supabase keys with excessive permissions
- Stripe secret keys in frontend code
- Sentry DSN with embedded tokens
- Analytics tokens in frontend code
- Service credentials in frontend bundles
- Feature flags containing service credentials
- GraphQL endpoints with authentication tokens in client code
- Webhook secrets in frontend code
- Third-party API keys in frontend code
- Environment variables exposed to client bundle (process.env.*)

### Source Maps and Build Artifacts
- Exposed source maps in production
- Source maps accessible without authentication
- Source maps revealing internal API structure
- Source maps revealing environment variables
- Source maps in publicly accessible build directories
- Compiled source code in build artifacts
- Minification without source map protection

### Browser Storage
- Sensitive data in localStorage (accessible to XSS)
- JWT tokens in localStorage
- User credentials in localStorage
- Sensitive data in sessionStorage
- Tokens in sessionStorage
- Sensitive data in IndexedDB
- Sensitive data in cookies without HttpOnly
- Cached sensitive data in Service Worker Cache API
- Sensitive data in browser localStorage without expiration
- Cached API responses with sensitive data

### Third-Party Script Risks
- Third-party analytics scripts (data exfiltration risk)
- Third-party chat widgets (XSS risk)
- CDN scripts without Subresource Integrity (SRI)
- Untrusted CDN dependencies
- Third-party scripts with excessive permissions
- Third-party scripts loaded over HTTP
- Third-party scripts from compromised CDNs
- Third-party scripts accessing sensitive DOM elements
- Third-party form widgets handling sensitive data
- Third-party payment widgets handling credentials
- Missing CSP to restrict third-party scripts

### DOM Security
- DOM-based XSS (innerHTML, outerHTML, document.write with user input)
- Prototype pollution (Object.prototype pollution leading to XSS or RCE)
- Unsafe HTML rendering
- Unsafe markdown rendering
- Unsafe URL handling (javascript:, data:, vbscript: URIs)
- Insecure postMessage usage (missing origin validation)
- Insecure postMessage with wildcard origin
- Insecure service workers
- Cache leakage through service workers
- DOM clobbering
- Mutation-based XSS

### UI Trust Abuse
- Clickjacking (missing X-Frame-Options or CSP frame-ancestors)
- UI redress attacks
- Hidden disabled buttons bypassed via API
- Invisible form fields submitted
- Double-submit attacks
- UI manipulation through CSS injection
- Missing Content-Security-Policy allowing UI manipulation

### Debug and Development
- Debug tooling exposed in production (React DevTools, Vue DevTools)
- Exposed feature flags in production
- Development endpoints accessible in production
- Test accounts accessible in production
- Debug console accessible in production
- Performance profiling tools in production
- Source code exposed through error messages

### Browser Security
- Missing Content-Security-Policy
- Missing X-Frame-Options
- Missing X-Content-Type-Options
- Missing Referrer-Policy
- Missing Permissions-Policy
- Missing Cross-Origin-Opener-Policy
- Missing Cross-Origin-Embedder-Policy
- Missing Cross-Origin-Resource-Policy
- Insecure iframe embedding (allowing untrusted origins)
- Missing SRI on critical scripts

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
11. Test for prototype pollution
12. Check for client-side secrets leakage through build process
13. Verify third-party scripts are loaded securely
14. Check for UI trust abuse vectors

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| API key in frontend bundle | CRITICAL |
| Client-side payment validation only | HIGH |
| Sensitive data in localStorage | HIGH |
| DOM-based XSS | HIGH |
| Prototype pollution leading to XSS | HIGH |
| Exposed source maps in production | MEDIUM |
| Missing Subresource Integrity | MEDIUM |
| Debug tooling in production | LOW |
| Missing CSP | MEDIUM |

---

## Evidence Requirements

- Specific frontend file or component affected
- Whether the secret or sensitive data is accessible to all users
- Whether client-side checks can be bypassed via direct API calls
- Browser storage location of sensitive data
- Whether the finding is exploitable through user interaction
