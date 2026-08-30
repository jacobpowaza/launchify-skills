# Logging, Monitoring, and Response

**Category ID:** `logging`

---

## Scope

Inspect all logging configurations, monitoring, alerting, incident response, and security operations.

---

## Checks

### Logging Security
- Exposed logs
- Sensitive data in logs
- API keys in logs
- Passwords in logs
- Tokens in logs
- PII in logs
- Missing audit logs
- Missing log retention policy
- Missing log integrity controls
- Missing time synchronization

### Monitoring
- Missing security monitoring
- Missing anomaly detection
- Missing alerting
- Missing dependency monitoring
- Missing infrastructure monitoring
- Missing authentication monitoring
- Missing authorization-failure monitoring
- Missing payment-abuse monitoring
- Missing AI abuse monitoring
- Missing data-exfiltration monitoring

### Incident Response
- Missing incident-response planning
- No incident response plan
- No breach notification process
- Missing breach escalation paths
- Missing incident ownership
- Missing security ownership
- No security owner for critical systems
- Missing alert triage and severity
- Missing forensic preservation
- Missing incident runbooks
- Missing tabletop exercises
- Missing post-incident review
- Missing customer communication process
- Missing regulatory notification process

### Security Operations
- Missing security testing strategy
- Missing threat modeling
- Missing penetration testing
- No staging security parity
- Staging configuration materially weaker than production
- Security controls disabled in staging
- Production-only behavior not tested before release

---

## Methodology

1. Verify audit logging is enabled for security-sensitive operations
2. Check logs for sensitive data leakage
3. Verify monitoring and alerting covers critical security events
4. Verify incident response plan exists and is documented
5. Check for security ownership and escalation paths
6. Verify staging security parity with production
7. Check for threat modeling and penetration testing
8. Verify log retention and integrity controls
9. Check for anomaly detection
10. Verify post-incident review process

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| PII in logs | HIGH |
| Missing incident response plan | HIGH |
| No security monitoring | HIGH |
| Missing audit logs for sensitive operations | MEDIUM |
| Staging weaker than production | MEDIUM |
| Missing log retention policy | LOW |

---

## Evidence Requirements

- Logging technology and configuration
- Whether sensitive data is logged
- Whether monitoring covers critical events
- Whether incident response processes exist
- Whether staging matches production security
