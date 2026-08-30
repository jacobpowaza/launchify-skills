# Deployment Security

**Category ID:** `deployment`

---

## Scope

Inspect all deployment configurations, deployment pipelines, environment management, and deployment safety controls.

---

## Checks

### Deployment Configuration
- Insecure deployment defaults
- Production deployment without review
- Production deployment without rollback
- Missing blue-green or canary controls where required
- Missing health checks
- Missing readiness checks
- Missing liveness checks
- Missing graceful shutdown

### Migration and Configuration
- Missing migration coordination
- Deployment order failures
- Configuration drift
- Environment parity failures
- Staging not representative of production
- Missing deployment audit logs

### Artifact Security
- Missing artifact integrity verification
- Unsigned artifacts
- Mutable deployment artifacts
- Unpinned images
- Unpinned build dependencies

### Access Control
- Deployment credentials with excessive permissions
- Direct production access from developer machines
- Missing break-glass controls
- Missing disaster recovery deployment procedure
- Missing infrastructure drift detection
- Missing rollback testing

---

## Methodology

1. Inspect deployment configuration files (Docker Compose, Kubernetes manifests, Terraform, etc.)
2. Verify health, readiness, and liveness checks are configured
3. Verify rollback procedures exist and are documented
4. Check environment parity between staging and production
5. Verify migration coordination is handled
6. Check artifact integrity and signing
7. Verify deployment credentials follow least privilege
8. Check for direct production access from developer machines
9. Verify disaster recovery deployment procedures exist
10. Verify rollback testing is performed

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Production deployment without rollback | HIGH |
| Direct production access from developer machines | HIGH |
| Missing health checks | MEDIUM |
| Staging not representative of production | MEDIUM |
| Mutable deployment artifacts | MEDIUM |
| Missing rollback testing | LOW |

---

## Evidence Requirements

- Deployment technology and target environment
- Specific configuration or pipeline step affected
- Whether the finding is in code or runtime state
- Impact on deployment safety and reliability
