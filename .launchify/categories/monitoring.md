# Monitoring

**Category ID:** `monitoring`

---

## Scope

Inspect monitoring, alerting, observability, and operational visibility across the application and infrastructure.

---

## Checks

### Application Monitoring
- Missing application performance monitoring
- Missing error tracking
- Missing request tracing
- Missing distributed tracing
- Missing custom metrics for business operations
- Missing availability monitoring
- Missing latency monitoring
- Missing throughput monitoring
- Missing saturation monitoring

### Security Monitoring
- Missing authentication monitoring
- Missing authorization-failure monitoring
- Missing payment-abuse monitoring
- Missing AI abuse monitoring
- Missing data-exfiltration monitoring
- Missing anomaly detection
- Missing intrusion detection

### Infrastructure Monitoring
- Missing infrastructure monitoring
- Missing container monitoring
- Missing Kubernetes monitoring
- Missing cloud audit-log collection
- Missing resource utilization monitoring
- Missing capacity planning data

### Alerting
- Missing alerting
- Missing alert severity levels
- Missing alert triage
- Missing on-call rotation
- Missing escalation paths
- Alert fatigue from noisy alerts

---

## Methodology

1. Verify application performance monitoring is configured
2. Check error tracking and alerting
3. Verify security event monitoring
4. Check infrastructure monitoring coverage
5. Verify alerting rules exist for critical events
6. Check for on-call and escalation procedures
7. Verify monitoring covers all environments (production, staging)
8. Check for custom business metrics
9. Verify distributed tracing is configured
10. Check for capacity planning data

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No security monitoring | HIGH |
| No application monitoring in production | HIGH |
| Missing alerting on authentication failures | MEDIUM |
| Missing infrastructure monitoring | MEDIUM |
| Missing custom business metrics | LOW |

---

## Evidence Requirements

- Monitoring technology and configuration
- What events are monitored
- What alerts are configured
- Whether monitoring covers all critical systems
- Whether alerting and escalation are operational
