# Incident Response

**Category ID:** `incident-response`

---

## Scope

Inspect incident response planning, procedures, escalation, and operational readiness for security incidents. It's not if you'll have an incident, it's when — without preparation, incidents become catastrophes.

---

## Checks

### Planning
- No incident response plan
- Missing breach notification process
- Missing breach escalation paths
- Missing incident ownership
- Missing security ownership
- No security owner for critical systems
- Missing incident classification criteria
- Missing incident severity levels
- Missing incident response SLAs

### Procedures
- Missing incident runbooks for common scenarios (data breach, DDoS, ransomware, etc.)
- Missing forensic preservation procedures
- Missing time synchronization for log correlation
- Missing post-incident review process
- Missing tabletop exercises
- Missing customer communication process
- Missing regulatory notification process (GDPR 72-hour, CCPA, etc.)
- Missing chain of custody procedures
- Missing evidence preservation
- Missing incident documentation standards

### Operational Readiness
- Missing dependency monitoring
- Missing vulnerability remediation process
- Missing risk acceptance process
- Missing security exception expiration
- Missing security metrics
- Missing security documentation
- Missing security training
- Missing security champions program
- Missing security on-call rotation

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
11. Verify runbooks are tested and up to date
12. Check for incident response exercises

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No incident response plan | HIGH |
| No security ownership for critical systems | HIGH |
| Missing breach notification process | MEDIUM |
| Missing incident runbooks | MEDIUM |
| Missing post-incident review | LOW |
| Missing tabletop exercises | LOW |

---

## Evidence Requirements

- Incident response process affected
- Whether the gap affects incident handling capability
- Impact on security operations
- Whether the gap affects regulatory compliance
