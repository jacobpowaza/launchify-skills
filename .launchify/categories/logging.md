# Logging, Monitoring, and Response

**Category ID:** `logging`

---

## Scope

Inspect all logging configurations, sensitive data in logs, audit logging, monitoring, alerting, incident response, and security operations. Logs are both a security control and a liability — poorly managed logs leak secrets; missing logs make incident response impossible.

---

## Checks

### Sensitive Data in Logs
- Passwords logged in request/response logs
- API keys logged in request headers
- JWT tokens logged in authorization headers
- Bearer tokens logged in request logs
- Session tokens logged
- Credit card numbers logged
- PII logged without consent (emails, names, addresses, SSNs)
- Health data logged without authorization
- Payment data logged
- Database credentials logged
- Encryption keys logged
- Webhook signing secrets logged
- OAuth tokens logged
- Refresh tokens logged
- File content logged (uploaded files)
- Request bodies logged with sensitive fields
- Error messages containing secrets
- Stack traces exposing environment variables
- Internal URLs with credentials logged
- Third-party service credentials logged

### Log Exposure
- Exposed log files (accessible without authentication)
- Logs stored in publicly accessible storage
- Logs accessible through debug endpoints
- Logs in cloud storage without access controls
- Logs in shared logging infrastructure without tenant isolation
- Logs containing secrets in CI/CD output
- Logs shipped to third-party services without data protection
- Logs retained indefinitely without policy
- Log files not encrypted at rest
- Log files not encrypted in transit

### Audit Logging
- Missing audit logs for authentication events (login, logout, failed login)
- Missing audit logs for authorization events (access denied, privilege escalation)
- Missing audit logs for data access (read, write, delete)
- Missing audit logs for configuration changes
- Missing audit logs for admin operations
- Missing audit logs for payment events
- Missing audit logs for data export
- Missing audit logs for user management (create, update, delete)
- Missing audit logs for API key management
- Missing audit logs for security events
- Missing audit log integrity controls (tamper-evident)
- Missing audit log retention policies
- Missing audit log monitoring and alerting
- Audit logs not immutable
- Audit logs modifiable by administrators
- Missing time synchronization for log correlation

### Log Management
- Missing log retention policy
- Missing log rotation
- Missing log compression
- Missing log archival
- Missing log integrity controls
- Missing log aggregation
- Missing centralized logging
- Missing log search capability
- Missing log alerting
- Missing log-based anomaly detection
- Missing log-based threat detection
- Missing log correlation across services
- Missing log format standardization
- Missing log severity levels
- Missing log context (request ID, user ID, trace ID)

---

## Methodology

1. Verify audit logging is enabled for security-sensitive operations
2. Check logs for sensitive data leakage (passwords, tokens, PII, keys)
3. Verify monitoring and alerting covers critical security events
4. Verify incident response plan exists and is documented
5. Check for security ownership and escalation paths
6. Verify staging security parity with production
7. Check for threat modeling and penetration testing
8. Verify log retention and integrity controls
9. Check for anomaly detection
10. Verify post-incident review process
11. Check log storage access controls
12. Verify log encryption at rest and in transit
13. Check for centralized log aggregation
14. Verify time synchronization across services

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Passwords logged in plaintext | CRITICAL |
| API keys in logs | HIGH |
| PII in logs | HIGH |
| Exposed log files with sensitive data | HIGH |
| Missing audit logs for authentication events | HIGH |
| Missing incident response plan | HIGH |
| No security monitoring | HIGH |
| Missing audit logs for admin operations | MEDIUM |
| Staging weaker than production | MEDIUM |
| Missing log retention policy | LOW |
| Missing log aggregation | LOW |

---

## Evidence Requirements

- Logging technology and configuration
- Whether sensitive data is logged
- Whether monitoring covers critical events
- Whether incident response processes exist
- Whether staging matches production security
- Whether logs are encrypted and access-controlled
