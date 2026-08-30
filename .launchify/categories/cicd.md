# CI/CD Security

**Category ID:** `cicd`

---

## Scope

Inspect all CI/CD pipelines, build configurations, deployment automation, and CI/CD-specific security controls.

---

## Checks

### Pipeline Security
- Insecure CI/CD
- Exposed CI secrets
- Untrusted GitHub Actions
- Unpinned build actions
- Untrusted third-party CI plugins
- Excessive build permissions
- Missing branch protection
- Missing review requirements

### Build Security
- Security checks failing open
- Missing artifact signing
- Missing deployment auditing
- Pull requests from forks receiving secrets
- Unsafe script interpolation
- Command injection in CI variables
- Untrusted checkout behavior
- Mutable action references
- Build artifacts overwritten without verification
- Missing isolated build environments
- Build runners with excessive network access
- Persistent compromised runners

### Release Security
- Missing provenance
- Missing release approvals
- Missing separation between build and deploy identities
- Missing rollback automation
- Missing CI log redaction
- Secrets exposed through test output
- Dependency installation from untrusted sources
- Deployment triggered by untrusted branches
- Missing environment protection rules

---

## Methodology

1. Inspect all CI/CD configuration files (GitHub Actions, GitLab CI, Jenkins, etc.)
2. Check for secrets exposure in CI variables and logs
3. Verify build actions are pinned to specific versions
4. Check for command injection in CI variables
5. Verify branch protection and review requirements
6. Check for artifact signing and provenance
7. Verify environment protection rules for production deployments
8. Check for fork PR secret exposure
9. Verify build runners have minimal access
10. Check for CI log redaction of sensitive data

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| CI secrets exposed in logs | CRITICAL |
| Command injection in CI variable | CRITICAL |
| Production deployment without review | HIGH |
| Unpinned build actions | MEDIUM |
| Missing artifact signing | MEDIUM |
| Missing CI log redaction | LOW |

---

## Evidence Requirements

- CI/CD platform and pipeline affected
- Specific workflow, job, or step affected
- Whether secrets are exposed
- Whether build integrity can be compromised
- Impact on deployment safety
