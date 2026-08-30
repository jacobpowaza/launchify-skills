# Monitoring

**Category ID:** `monitoring`

---

## Scope

Inspect monitoring, alerting, observability, and operational visibility across the application and infrastructure. You cannot stop what you cannot see — monitoring is the difference between detecting a breach in minutes versus months.

---

## Checks

### Application Monitoring
- Missing application performance monitoring (APM)
- Missing error tracking (Sentry, Bugsnag, Datadog)
- Missing request tracing
- Missing distributed tracing (OpenTelemetry, Jaeger, Zipkin)
- Missing custom metrics for business operations
- Missing availability monitoring (uptime)
- Missing latency monitoring (response times)
- Missing throughput monitoring (requests per second)
- Missing saturation monitoring (queue depth, thread pool usage)
- Missing SLA/SLO monitoring
- Missing error rate monitoring
- Missing dependency latency monitoring

### Security Monitoring
- Missing threat intelligence feed integration
- Missing indicators of compromise (IoC) monitoring
- Missing network traffic anomaly detection
- Missing user behavior analytics (UBA)
- Missing deception technology (honeypots/honeytokens)
- Missing dark web monitoring for leaked credentials
- Missing authentication monitoring (failed logins, brute force detection)
- Missing authorization-failure monitoring (access denied events)
- Missing payment-abuse monitoring (duplicate refunds, price manipulation)
- Missing AI abuse monitoring (token abuse, prompt injection attempts, cost spikes)
- Missing data-exfiltration monitoring (large data exports, unusual queries)
- Missing anomaly detection (unusual patterns in traffic, users, or data access)
- Missing intrusion detection (IDS/IPS)
- Missing SIEM integration
- Missing security event correlation
- Missing threat intelligence feeds
- Missing brute force detection
- Missing account takeover detection
- Missing credential stuffing detection
- Missing privilege escalation detection
- Missing data access anomaly detection

### Infrastructure Monitoring
- Missing infrastructure monitoring (CPU, memory, disk, network)
- Missing container monitoring (Docker, containerd)
- Missing Kubernetes monitoring (pod health, node health, cluster health)
- Missing cloud audit-log collection (CloudTrail, Audit Logs)
- Missing resource utilization monitoring
- Missing capacity planning data
- Missing network monitoring
- Missing DNS monitoring
- Missing certificate expiration monitoring
- Missing dependency health monitoring

### Alerting
- Missing alerting
- Missing alert severity levels (P0, P1, P2, P3)
- Missing alert routing (right team, right channel)
- Missing alert escalation
- Missing on-call rotation
- Missing escalation paths
- Alert fatigue from noisy alerts
- Missing alert suppression during maintenance
- Missing alert deduplication
- Missing alert correlation
- Missing runbook links in alerts
- Missing alert testing

### Business Monitoring
- Missing revenue monitoring
- Missing conversion funnel monitoring
- Missing user activity monitoring
- Missing feature adoption monitoring
- Missing error impact monitoring
- Missing cost monitoring (API calls, infrastructure spend)

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
11. Verify security-specific monitoring exists
12. Check for anomaly detection
13. Verify alert severity and routing

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No security monitoring | HIGH |
| No application monitoring in production | HIGH |
| Missing alerting on authentication failures | MEDIUM |
| Missing anomaly detection for data access | MEDIUM |
| Missing brute force detection | MEDIUM |
| Missing infrastructure monitoring | MEDIUM |
| Missing custom business metrics | LOW |
| Missing alert severity levels | LOW |

---

## Evidence Requirements

- Monitoring technology and configuration
- What events are monitored
- What alerts are configured
- Whether monitoring covers all critical systems
- Whether alerting and escalation are operational
- Whether security monitoring exists separate from application monitoring
