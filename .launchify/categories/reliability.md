# Reliability and Recovery

**Category ID:** `reliability`

---

## Scope

Inspect all reliability controls, recovery mechanisms, resilience patterns, and operational readiness.

---

## Checks

### Backup and Recovery
- Missing backups
- Untested restoration
- Missing disaster recovery
- Missing failover
- Missing regional recovery
- Missing restore testing

### Rate Limiting and Resource Protection
- Missing rate-limit fallback
- Missing service timeouts
- Infinite retries
- Resource exhaustion
- Denial-of-service risks
- Queue poisoning
- Retry storms
- Unbounded concurrency
- Unbounded uploads
- Unbounded queries
- Unsafe retry of non-idempotent operations
- Missing idempotency

### Resilience Patterns
- Missing circuit breakers
- Missing bulkheads
- Missing graceful degradation
- Missing health checks
- Missing readiness checks
- Missing liveness checks
- Missing dependency failure handling
- Missing queue dead-letter handling
- Missing poison-message handling
- Missing backpressure

### Resource Limits
- Missing connection limits
- Missing memory limits
- Missing CPU limits
- Missing disk limits
- Missing request-size limits
- Missing response-size limits
- Missing pagination

### Data Integrity
- Missing cache invalidation
- Stale cache authorization
- Data corruption risks
- Partial transaction failures
- Distributed transaction failures
- Missing reconciliation

### Operational Readiness
- Missing recovery runbooks
- Missing operational ownership
- Missing service-level objectives
- Missing error budgets
- Missing capacity planning
- Missing dependency failover

---

## Methodology

1. Verify backup and restoration procedures exist and are tested
2. Check for disaster recovery and failover mechanisms
3. Test rate limiting and resource protection
4. Verify circuit breakers, bulkheads, and graceful degradation
5. Check health, readiness, and liveness checks
6. Verify idempotency on non-idempotent operations
7. Check for bounded resource usage (queries, concurrency, uploads)
8. Verify cache invalidation and authorization
9. Check for reconciliation and data integrity controls
10. Verify operational runbooks and ownership

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No backup or restoration procedure | CRITICAL |
| Missing rate limiting on critical endpoint | HIGH |
| Unbounded queries causing resource exhaustion | HIGH |
| Missing circuit breaker on external dependency | MEDIUM |
| Missing health checks | MEDIUM |
| Missing capacity planning | LOW |

---

## Evidence Requirements

- System component affected
- Reliability pattern that is missing
- Impact on availability and data integrity
- Whether recovery procedures are tested
- Whether resource limits are configured
