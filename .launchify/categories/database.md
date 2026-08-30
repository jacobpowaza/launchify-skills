# Database and Data-Access Security

**Category ID:** `database`

---

## Scope

Inspect all database configurations, queries, data access patterns, migrations, encryption, and data protection mechanisms.

---

## Checks

### Database Exposure
- Open database permissions
- Excessive database permissions
- Public database exposure
- Weak database authentication
- Excessive database access
- Unrestricted administrative database access
- Database credentials shared across services unnecessarily
- Weak database segmentation

### Injection Vulnerabilities
- SQL injection
- NoSQL injection
- Database command injection
- Unsafe queries
- Missing query parameterization
- Unsafe dynamic query construction

### Data Protection
- Sensitive data exposure
- Exposed database backups
- Missing encryption at rest
- Missing encryption in transit
- Missing database audit logs
- Missing data masking
- Missing field-level encryption where required
- Sensitive data copied into development or staging

### Query Safety
- Unbounded queries
- Missing query timeouts
- Missing connection limits
- Database denial-of-service risks

### Migration Safety
- Unsafe migrations
- Destructive migrations without rollback
- Missing migration integrity checks

### Row-Level Security
- Missing row-level security where required
- Missing tenant filters

---

## Methodology

1. Identify all database connection strings and credentials
2. Inspect database permission models and access controls
3. Trace all database queries for injection vulnerabilities
4. Verify query parameterization is used consistently
5. Check for unbounded queries, missing timeouts, missing connection limits
6. Inspect encryption at rest and in transit configuration
7. Verify tenant isolation at the database level
8. Inspect migration files for destructive operations
9. Check for sensitive data in non-production environments
10. Verify database audit logging is enabled

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| SQL injection | CRITICAL |
| Missing tenant isolation | CRITICAL |
| Database publicly accessible | CRITICAL |
| Missing encryption at rest for PII | HIGH |
| Unbounded queries | MEDIUM |
| Missing database audit logs | MEDIUM |

---

## Evidence Requirements

- Database technology and configuration
- Specific query or access pattern affected
- Whether injection is exploitable through application input
- Whether tenant isolation is affected
- Data sensitivity levels involved
