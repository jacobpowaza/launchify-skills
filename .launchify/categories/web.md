# Web Application Security

**Category ID:** `web`

---

## Scope

Inspect all web application security controls including XSS, CSRF, injection, file handling, cookie security, CORS, security headers, SSRF, XXE, and browser-side security. This category covers the full OWASP Top 10 and beyond.

---

## Checks

### Cross-Site Scripting (XSS)
- Reflected XSS (user input reflected in response without encoding)
- Stored XSS (malicious script stored in database and served to users)
- DOM-based XSS (client-side JavaScript processes untrusted input unsafely)
- Mutation-based XSS (browser DOM mutation creates XSS vector)
- Unsafe template rendering (Handlebars, EJS, Pug, Jinja2, Blade)
- Server-side template injection (SSTI)
- Unsafe innerHTML / innerText usage
- Unsafe document.write usage
- Unsafe eval() with user input
- Unsafe setTimeout/setInterval with string argument
- Unsafe HTML rendering from Markdown
- Unsafe URL handling (javascript:, data: URIs)
- Unsafe postMessage handling without origin validation
- Unsafe iframe srcdoc
- SVG-based XSS
- CSS expression-based XSS

### Cross-Site Request Forgery (CSRF)
- Missing anti-CSRF tokens on state-changing requests
- Missing SameSite cookie attribute
- CSRF on password change
- CSRF on email change
- CSRF on account deletion
- CSRF on payment operations
- CSRF on admin operations
- CSRF on file upload
- CSRF through JSON API (content-type confusion)
- CSRF token in URL (logged by proxies)
- CSRF token not validated
- CSRF token predictable

### Injection
- Command injection (OS command execution through user input)
- Code injection (eval, Function constructor with user input)
- LDAP injection
- XPath injection
- Expression Language injection
- Header injection (CRLF injection)
- Unsafe deserialization (pickle, yaml.load, eval)
- Prototype pollution (Object.assign, merge, deep merge with user input)
- Prototype pollution leading to XSS or RCE

### Path Traversal and File System
- Path traversal (../../etc/passwd)
- Directory traversal
- File inclusion (local and remote)
- Unsafe file path construction
- Zip-slip (path traversal in archive extraction)
- Missing upload directory isolation
- Upload directory accessible without authentication
- Symlink attacks
- Missing decompression limits (zip bomb)
- Missing upload size limits
- Missing file count limits

### Server-Side Request Forgery (SSRF)
- SSRF to internal services (127.0.0.1, localhost, internal hostnames)
- SSRF to cloud metadata endpoints (169.254.169.254)
- SSRF to internal APIs without authentication
- SSRF through URL parameters
- SSRF through webhook URLs
- SSRF through file import (SVG, XML)
- SSRF through PDF generation
- SSRF through HTML-to-image conversion
- SSRF bypass techniques (IP encoding, DNS rebinding, IPv6)
- SSRF to internal databases
- SSRF to internal message queues
- SSRF to internal caching services
- SSRF to internal authentication services
- Blind SSRF (no response returned)
- SSRF leading to credential theft

### XXE (XML External Entity)
- XXE through XML parsing
- XXE through SOAP
- XXE through SVG file processing
- XXE through DOCX/XLSX processing
- Blind XXE (no error output, but data exfiltrated)
- XXE to SSRF

### File Upload Security
- Insecure file uploads (unrestricted file type)
- Missing file type validation (client-side only)
- Missing malware scanning
- Unsafe file processing
- Unsafe archive extraction
- Missing file size limits
- Missing file count limits
- Uploaded files executable
- Uploaded files accessible without authentication
- Missing upload directory isolation
- File upload leading to RCE
- File upload leading to XSS
- Double extension bypass (image.php.jpg)
- MIME type not validated
- Missing content-type validation
- Missing file content validation
- Null byte injection in filename

### Security Headers
- Missing Content-Security-Policy (CSP) header
- Missing X-Frame-Options header
- Missing X-Content-Type-Options header
- Missing X-XSS-Protection header (legacy but still useful)
- Missing Strict-Transport-Security (HSTS) header
- Missing Referrer-Policy header
- Missing Permissions-Policy header
- Missing Cross-Origin-Opener-Policy (COOP) header
- Missing Cross-Origin-Embedder-Policy (COEP) header
- Missing Cross-Origin-Resource-Policy (CORP) header
- Missing Cache-Control headers on sensitive responses
- Missing Pragma header
- HSTS header without includeSubDomains
- HSTS header without preload
- CSP header too permissive (unsafe-inline, unsafe-eval)
- CSP header missing directive for scripts

### Cookie Security
- Missing HttpOnly flag on session cookies
- Missing Secure flag on cookies
- Missing SameSite attribute on cookies
- Session cookie with SameSite=None without justification
- Cookie with excessively long expiration
- Sensitive data in cookies
- Cookie scope too broad (domain, path)
- Missing cookie prefix (__Host-, __Secure-)
- Cookie not regenerated after login
- Cookie persists after password change

### CORS Configuration
- Permissive CORS (Access-Control-Allow-Origin: *)
- CORS with credentials and wildcard origin
- CORS reflecting Origin header without validation
- Missing Origin validation
- CORS misconfiguration allowing subdomain takeover
- Missing CORS preflight handling
- Excessive CORS headers

### Redirects and Navigation
- Open redirect (user-controlled redirect URL)
- Open redirect through login flow
- Open redirect through OAuth callback
- Open redirect through error pages
- Directory listing exposed
- Missing index.html or default document

### Caching and Headers
- Cache poisoning (manipulating cache key)
- Cache-control failures on sensitive responses
- Host-header injection
- Request smuggling (CL.TE, TE.CL, TE.TE)
- Response splitting (HTTP header injection)
- Missing cache-control on authenticated responses
- Sensitive data cached by proxy or CDN

### Browser Security
- Clickjacking (missing X-Frame-Options or CSP frame-ancestors)
- UI redress attacks
- Missing Content-Type sniffing protection
- Unsafe iframe embedding (allowed from untrusted origins)
- Browser history leakage
- Referrer leakage of sensitive URLs
- Sensitive information disclosure in error pages

---

## Methodology

1. Test all user inputs for XSS (reflected, stored, DOM-based)
2. Test all forms and state-changing requests for CSRF
3. Test all file upload functionality for malicious file types
4. Test URL parameters for SSRF
5. Test XML parsers for XXE
6. Test cookie settings for HttpOnly, Secure, SameSite
7. Verify security headers are present (CSP, X-Frame-Options, X-Content-Type-Options, HSTS)
8. Test CORS configuration for permissive origins
9. Test open redirects
10. Test path traversal and directory listing
11. Test template rendering for injection
12. Test deserialization for unsafe patterns
13. Test command injection vectors
14. Test prototype pollution vectors
15. Test for cache poisoning
16. Test for request smuggling

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Stored XSS | CRITICAL |
| Reflected XSS on authenticated page | HIGH |
| DOM-based XSS | HIGH |
| SSRF reaching internal services | CRITICAL |
| SSRF reaching cloud metadata | CRITICAL |
| Command injection | CRITICAL |
| CSRF on password change or payment | HIGH |
| CSRF on state-changing action | HIGH |
| Path traversal to sensitive files | HIGH |
| File upload leading to RCE | CRITICAL |
| XXE leading to data exfiltration | HIGH |
| Open redirect | MEDIUM |
| Missing security headers | MEDIUM |
| Missing HSTS | MEDIUM |
| Permissive CORS | MEDIUM |
| Missing SameSite cookie | LOW |

---

## Evidence Requirements

- Specific URL, form, or input vector affected
- Payload or proof-of-concept
- Whether the finding requires user interaction
- Impact on data confidentiality, integrity, or availability
- Whether the finding is exploitable through unauthenticated access
