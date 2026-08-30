# Database and Data-Access Security

**Category ID:** `database`

---

## Scope

Inspect all database configurations, queries, data access patterns, migrations, encryption, permissions, row-level security, and data protection mechanisms. The database is the crown jewel — if it is compromised, all data is exposed.

---

## Checks

### Injection Vulnerabilities
- SQL injection (classic, blind, second-order, time-based)
- SQL injection through ORDER BY, LIMIT, OFFSET clauses
- SQL injection through LIKE patterns
- SQL injection through UNION-based extraction
- SQL injection through stacked queries
- SQL injection through second-order (stored in DB, triggered later)
- NoSQL injection (MongoDB operators, $where, $gt, $regex)
- NoSQL injection through query operators in JSON
- LDAP injection
- XPath injection
- ORM injection (Sequelize, ActiveRecord, SQLAlchemy raw queries)
- Query builder injection (raw query methods in ORMs)
- Database command injection (xp_cmdshell, mongo shell commands)
- Unsafe dynamic query construction
- Missing query parameterization
- String concatenation in SQL queries
- Template literals in SQL queries

### Database Permissions
- Excessive database permissions (application user with DBA privileges)
- Database user with GRANT ALL on all tables
- Database user with CREATE, DROP, ALTER privileges when not needed
- Database user with GRANT OPTION
- Database user with SUPER, PROCESS, RELOAD privileges
- Shared database credentials across services
- Same database user for read and write operations
- Missing database user role separation
- Missing database-level audit logging
- Database accessible from 0.0.0.0/0
- Database accessible from public internet
- Database accessible from untrusted networks
- Missing IP allowlisting for database connections
- Missing SSL/TLS for database connections
- Database credentials in environment variables visible to all processes
- Database credentials shared between environments
- Default database credentials unchanged
- Weak database password

### Row-Level Security
- Missing row-level security (RLS) where required
- Missing tenant filters in database queries
- RLS policies not covering all access patterns
- RLS policies not enforced at database level (only app level)
- Missing column-level permissions
- Service account bypassing RLS
- Direct database access bypassing application authorization
- Database views not respecting RLS
- Stored procedures not respecting RLS
- Missing row-level security for multi-tenant tables
- Tenant ID not included in RLS policies
- RLS policies not tested

### Cryptographic Enforcement
- Database connections not enforcing TLS (rejecting unencrypted connections)
- Missing mutual TLS (mTLS) for service-to-database auth
- Redis/Memcached connections not encrypted in transit
- Elasticsearch/OpenSearch not enforcing TLS
- Kafka/RabbitMQ message queues not encrypted in transit
- Database backups not encrypted at rest
- Missing field-level encryption for PII columns
- Missing envelope encryption for cloud KMS
- Encryption key access not audited
- Missing customer-managed encryption keys (CMEK) where required

### Data Protection
- Sensitive data exposure in database responses
- Exposed database backups
- Missing encryption at rest for sensitive data
- Missing encryption in transit for database connections
- Missing field-level encryption for highly sensitive data (SSN, credit cards)
- Missing data masking in non-production environments
- Sensitive data copied into development or staging without masking
- Missing database audit logs
- Missing data classification
- Password hashes stored with weak algorithms
- API keys stored in plaintext in database
- Tokens stored in plaintext in database
- PII stored without encryption
- Payment card data stored without PCI compliance
- Health data stored without HIPAA compliance

### Query Safety
- Unbounded queries (no LIMIT clause)
- Missing query timeouts
- Missing connection limits
- Database denial-of-service risks through expensive queries
- Missing pagination on list endpoints
- Missing cursor-based pagination for large datasets
- N+1 query patterns
- Missing query result caching where appropriate
- Missing database connection pooling
- Missing query optimization
- Missing index usage

### Migration Safety
- Unsafe migrations (DROP COLUMN, DROP TABLE without backup)
- Destructive migrations without rollback
- Missing migration integrity checks
- Migrations that lock tables in production
- Migrations without data validation
- Migrations without testing on production-size data
- Missing migration ordering
- Missing migration dependency tracking

### Tenant Isolation
- Missing tenant isolation at database level
- Shared database without row-level security
- Missing tenant-aware queries
- Missing tenant-aware indexes
- Missing tenant-aware backups
- Cross-tenant joins possible
- Missing tenant-aware audit logging

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
11. Check row-level security policies where applicable
12. Verify column-level permissions for sensitive fields
13. Test for SQL injection through all user inputs
14. Check database user permissions against least privilege
15. Verify database network restrictions

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| SQL injection | CRITICAL |
| NoSQL injection | CRITICAL |
| Database publicly accessible | CRITICAL |
| Missing tenant isolation | CRITICAL |
| Database user with DBA privileges | HIGH |
| Missing encryption at rest for PII | HIGH |
| Missing row-level security | HIGH |
| Database accessible from 0.0.0.0/0 | HIGH |
| Default database credentials | HIGH |
| Unbounded queries | MEDIUM |
| Missing database audit logs | MEDIUM |
| Missing connection limits | MEDIUM |

---

## Evidence Requirements

- Database technology and configuration
- Specific query or access pattern affected
- Whether injection is exploitable through application input
- Whether tenant isolation is affected
- Data sensitivity levels involved
- Whether database permissions exceed least privilege
- Whether row-level security is enforced
