# Web Application Security

**Category ID:** `web`

---

## Scope

Inspect all web application security controls including XSS, CSRF, injection, file handling, cookie security, CORS, and browser-side security.

---

## Checks

### Cross-Site Scripting (XSS)
- XSS (Reflected, Stored, DOM-based)
- Unsafe template rendering
- Server-side template injection
- Unsafe HTML rendering
- Unsafe markdown rendering
- Unsafe URL handling
- Unsafe postMessage handling

### Cross-Site Request Forgery (CSRF)
- CSRF vulnerabilities
- Missing anti-CSRF tokens
- Missing SameSite cookie attribute

### Injection
- Command injection
- Unsafe deserialization
- Prototype pollution
- Path traversal

### Server-Side Request Forgery (SSRF)
- SSRF vulnerabilities
- XXE (XML External Entity)

### File Handling
- Insecure file uploads
- Missing malware or file scanning
- Unsafe file processing
- Unsafe archive extraction
- Zip-slip vulnerabilities
- Missing upload size limits
- Missing decompression limits

### Security Headers and Cookies
- Missing security headers
- Missing CSP (Content Security Policy)
- Clickjacking
- Insecure cookie settings
- Cookies missing HttpOnly, Secure, SameSite
- Missing anti-automation controls

### Redirects and Navigation
- Open redirects
- Path traversal
- Directory listing

### Caching and Headers
- Cache poisoning
- Cache-control failures
- CORS misconfiguration
- Permissive CORS
- Missing origin validation
- Host-header injection
- Request smuggling
- Response splitting

### Browser Security
- Unsafe iframe embedding
- Browser history leakage
- Referrer leakage
- Sensitive information disclosure

---

## Methodology

1. Test all user inputs for XSS (reflected, stored, DOM-based)
2. Test all forms and state-changing requests for CSRF
3. Test all file upload functionality for malicious file types
4. Test URL parameters for SSRF
5. Test XML parsers for XXE
6. Test cookie settings for HttpOnly, Secure, SameSite
7. Verify security headers are present (CSP, X-Frame-Options, X-Content-Type-Options, etc.)
8. Test CORS configuration for permissive origins
9. Test open redirects
10. Test path traversal and directory listing
11. Test template rendering for injection
12. Test deserialization for unsafe patterns

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Stored XSS | CRITICAL |
| SSRF reaching internal services | CRITICAL |
| Command injection | CRITICAL |
| CSRF on sensitive action | HIGH |
| Missing security headers | MEDIUM |
| Open redirect | MEDIUM |
| Missing SameSite cookie | LOW |

---

## Evidence Requirements

- Specific URL, form, or input vector affected
- Payload or proof-of-concept
- Whether the finding requires user interaction
- Impact on data confidentiality, integrity, or availability
