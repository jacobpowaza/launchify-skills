# CI/CD Security

**Category ID:** `cicd`

---

## Scope

Inspect all CI/CD pipelines, build configurations, deployment automation, and CI/CD-specific security controls. CI/CD is the crown jewel — compromising it means compromising every deployment.

---

## Checks

### Pipeline Security
- Insecure CI/CD configuration
- Exposed CI secrets in logs, artifacts, or environment
- Untrusted GitHub Actions (third-party actions without review)
- Unpinned build actions (using `@main` instead of `@sha`)
- Untrusted third-party CI plugins
- Excessive build permissions (write-all, admin tokens)
- Missing branch protection rules
- Missing review requirements for security-critical changes
- Missing required status checks
- Missing signed commits

### Build Security
- Security checks failing open (security scan failure doesn't block build)
- Missing artifact signing
- Missing deployment auditing
- Pull requests from forks receiving secrets
- Unsafe script interpolation (using env vars in shell scripts)
- Command injection in CI variables
- Untrusted checkout behavior
- Mutable action references
- Build artifacts overwritten without verification
- Missing isolated build environments
- Build runners with excessive network access
- Persistent compromised runners
- Secrets echoed in build logs
- Secrets in CI test output
- Secrets in CI coverage reports
- Secrets in CI artifact uploads

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
- Missing deployment approval gates
- Missing canary deployment controls
- Missing deployment rollback testing

---

## Methodology

1. Inspect all CI/CD configuration files (GitHub Actions, GitLab CI, Jenkins)
2. Check for secrets exposure in CI variables and logs
3. Verify build actions are pinned to specific versions
4. Check for command injection in CI variables
5. Verify branch protection and review requirements
6. Check for artifact signing and provenance
7. Verify environment protection rules for production deployments
8. Check for fork PR secret exposure
9. Verify build runners have minimal access
10. Check for CI log redaction of sensitive data
11. Verify security scans block builds on failure
12. Check for deployment approval gates

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| CI secrets exposed in logs | CRITICAL |
| Command injection in CI variable | CRITICAL |
| Production deployment without review | HIGH |
| Fork PRs receiving secrets | HIGH |
| Unpinned build actions | MEDIUM |
| Missing artifact signing | MEDIUM |
| Security checks failing open | HIGH |
| Missing CI log redaction | LOW |

---

## Evidence Requirements

- CI/CD platform and pipeline affected
- Specific workflow, job, or step affected
- Whether secrets are exposed
- Whether build integrity can be compromised
- Impact on deployment safety
