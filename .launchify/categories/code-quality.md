# Code Quality and Security Process

**Category ID:** `code-quality`

---

## Scope

Inspect code quality, security process maturity, testing practices, and development workflow security.

---

## Checks

### Code Review
- Unreviewed code
- Missing security review
- Missing secure coding guidance
- Missing code ownership for sensitive areas

### Security Testing
- Missing threat modeling
- No threat modeling
- Missing automated security tests
- Missing SAST
- Missing DAST
- Missing fuzz testing
- No penetration testing
- Missing security regression tests
- Missing abuse-case tests
- Missing authorization tests
- Missing tenant-isolation tests

### Vulnerability Management
- Dead vulnerable code
- Debug code
- Insecure TODO implementations
- Security controls disabled for development and accidentally enabled in production
- Missing vulnerability remediation process
- Missing security ownership
- Missing risk acceptance process
- Missing security exception expiration

### Process Maturity
- Missing secure design review
- Missing architecture review
- Missing release security checklist
- Missing staging security parity
- Missing incident-response exercises
- Missing security metrics
- Missing security documentation
- Missing security training
- Missing dependency monitoring

---

## Methodology

1. Check for security review in code review process
2. Verify automated security tests are in CI/CD
3. Check for threat modeling documentation
4. Verify SAST and DAST are configured
5. Check for security regression tests
6. Verify security ownership is assigned
7. Check for vulnerability remediation process
8. Verify staging security parity
9. Check for security metrics and reporting
10. Verify incident-response exercises are performed

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No security testing in CI/CD | HIGH |
| No threat modeling for critical systems | HIGH |
| Security controls disabled in production | HIGH |
| No security ownership | MEDIUM |
| Missing security regression tests | MEDIUM |
| Missing security documentation | LOW |

---

## Evidence Requirements

- Development process and tooling affected
- Security practice that is missing
- Whether the gap affects production systems
- Impact on security posture
