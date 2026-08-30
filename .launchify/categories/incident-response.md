# Incident Response

**Category ID:** `incident-response`

---

## Scope

Inspect incident response planning, procedures, escalation, and operational readiness for security incidents.

---

## Checks

### Planning
- No incident response plan
- Missing breach notification process
- Missing breach escalation paths
- Missing incident ownership
- Missing security ownership
- No security owner for critical systems

### Procedures
- Missing incident runbooks
- Missing forensic preservation
- Missing time synchronization for log correlation
- Missing post-incident review
- Missing tabletop exercises
- Missing customer communication process
- Missing regulatory notification process

### Operational Readiness
- Missing dependency monitoring
- Missing vulnerability remediation process
- Missing risk acceptance process
- Missing security exception expiration
- Missing security metrics
- Missing security documentation
- Missing security training

---

## Methodology

1. Verify incident response plan exists and is documented
2. Check for escalation paths and ownership
3. Verify incident runbooks exist for common scenarios
4. Check for forensic preservation capabilities
5. Verify post-incident review process
6. Check for tabletop exercises
7. Verify customer communication process
8. Check for regulatory notification process
9. Verify security training is performed
10. Check for security metrics and reporting

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No incident response plan | HIGH |
| No security ownership for critical systems | HIGH |
| Missing breach notification process | MEDIUM |
| Missing incident runbooks | MEDIUM |
| Missing post-incident review | LOW |

---

## Evidence Requirements

- Incident response process affected
- Whether the gap affects incident handling capability
- Impact on security operations
