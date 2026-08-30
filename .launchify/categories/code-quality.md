# Code Quality and Security Process

**Category ID:** `code-quality`

---

## Scope

Inspect code quality, security process maturity, testing practices, and development workflow security. Code quality is a security multiplier — poor code quality makes vulnerabilities harder to find and fix.

---

## Checks

### Code Review
- Unreviewed code (merged without review)
- Missing security review for sensitive changes
- Missing secure coding guidance
- Missing code ownership for sensitive areas
- Missing review requirements for security-critical files
- Missing two-person review for infrastructure changes
- Code review without security checklist

### Security Testing
- Missing threat modeling for critical systems
- No threat modeling
- Missing automated security tests
- Missing SAST (Static Application Security Testing)
- Missing DAST (Dynamic Application Security Testing)
- Missing fuzz testing
- No penetration testing
- Missing security regression tests
- Missing abuse-case tests
- Missing authorization tests
- Missing tenant-isolation tests
- Missing injection tests
- Missing authentication bypass tests
- Missing API security tests

### Vulnerability Management
- Dead vulnerable code (old code with known CVEs)
- Debug code left in production (console.log, debugger, var_dump)
- Insecure TODO implementations (e.g., TODO: add auth)
- Security controls disabled for development and accidentally enabled in production
- Missing vulnerability remediation process
- Missing security ownership
- Missing risk acceptance process
- Missing security exception expiration
- Missing vulnerability scanning in CI/CD
- Known vulnerabilities not remediated
- Missing dependency vulnerability monitoring
- Missing CVE tracking

### DevSecOps Maturity
- Missing secure coding training records
- Missing role-based security training
- Missing security awareness for developers
- Missing DevSecOps maturity assessment
- Missing security champions program
- Missing secure coding standards documentation

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
- Missing security champions program
- Missing secure coding standards
- Missing security coding guidelines

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
11. Check for debug code in production
12. Verify security training is conducted

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No security testing in CI/CD | HIGH |
| No threat modeling for critical systems | HIGH |
| Security controls disabled in production | HIGH |
| Debug code in production | MEDIUM |
| No security ownership | MEDIUM |
| Missing security regression tests | MEDIUM |
| Missing staging security parity | MEDIUM |
| Missing security documentation | LOW |

---

## Evidence Requirements

- Development process and tooling affected
- Security practice that is missing
- Whether the gap affects production systems
- Impact on security posture
