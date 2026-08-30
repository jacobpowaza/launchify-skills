# Reliability and Recovery

**Category ID:** `reliability`

---

## Scope

Inspect all reliability controls, recovery mechanisms, resilience patterns, and operational readiness. Reliability bugs become outages — the cost of downtime is measured in revenue, reputation, and regulatory compliance.

---

## Checks

### Backup and Recovery
- Missing backups (no backup configured)
- Untested restoration (backup exists but never verified)
- Missing disaster recovery plan
- Missing failover mechanism
- Missing regional recovery
- Missing restore testing schedule
- Missing backup encryption
- Missing backup access controls
- Backup containing secrets
- Missing point-in-time recovery
- Missing backup monitoring
- Missing backup alerting
- Backup retention too short or too long

### Rate Limiting and Resource Protection
- Missing rate-limit fallback (what happens when rate limiter is down)
- Missing service timeouts
- Infinite retries without backoff
- Exponential backoff not implemented
- Resource exhaustion (memory, connections, file handles)
- Denial-of-service risks
- Queue poisoning (poison message blocks queue processing)
- Retry storms (all clients retry simultaneously)
- Unbounded concurrency
- Unbounded uploads
- Unbounded queries
- Missing pagination
- Unsafe retry of non-idempotent operations
- Missing idempotency on critical operations
- Missing request-size limits
- Missing response-size limits

### Resilience Patterns
- Missing circuit breakers on external dependencies
- Missing bulkheads between services
- Missing graceful degradation
- Missing health checks
- Missing readiness checks
- Missing liveness checks
- Missing dependency failure handling
- Missing queue dead-letter handling
- Missing poison-message handling
- Missing backpressure
- Missing timeout on external calls
- Missing retry budget
- Missing fallback behavior
- Missing cached fallback for reads

### Resource Limits
- Missing connection limits
- Missing memory limits
- Missing CPU limits
- Missing disk limits
- Missing request-size limits
- Missing response-size limits
- Missing pagination on list operations
- Missing file upload size limits
- Missing concurrent connection limits
- Missing thread pool limits

### Data Integrity
- Missing cache invalidation strategy
- Stale cache serving stale authorization
- Data corruption risks
- Partial transaction failures
- Distributed transaction failures
- Missing reconciliation
- Missing data validation after writes
- Missing checksums on critical data
- Missing idempotency keys

### Operational Readiness
- Missing recovery runbooks
- Missing operational ownership
- Missing service-level objectives (SLOs)
- Missing error budgets
- Missing capacity planning
- Missing dependency failover
- Missing deployment rollback
- Missing feature flag infrastructure
- Missing kill switch for features

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
11. Verify retry logic with exponential backoff
12. Check for timeout configuration on external calls
13. Verify dead-letter queue handling

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No backup or restoration procedure | CRITICAL |
| Missing rate limiting on critical endpoint | HIGH |
| Unbounded queries causing resource exhaustion | HIGH |
| Missing circuit breaker on external dependency | MEDIUM |
| Missing health checks | MEDIUM |
| Infinite retries without backoff | MEDIUM |
| Missing idempotency on payment operations | HIGH |
| Missing capacity planning | LOW |

---

## Evidence Requirements

- System component affected
- Reliability pattern that is missing
- Impact on availability and data integrity
- Whether recovery procedures are tested
- Whether resource limits are configured
