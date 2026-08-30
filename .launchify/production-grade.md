# Production Grade Rules

**Launchify Production Grade Protocol — Canonical Reference**

---

## Purpose

Grade the entire project on production readiness across every measurable dimension. Produce a single letter grade, per-dimension scores, a detailed breakdown, and a prioritized remediation path. This is a full audit — it reads everything, grades everything, and fixes nothing.

---

## Production Grade Flow

### Phase 1: Repository Reconnaissance

Establish a complete repository model (same as spec.md Phase 1). Then additionally identify:
- deployment target(s) and environment(s)
- expected SLA / uptime requirements (from docs, config, or code)
- user-facing surface area (routes, pages, components, commands)
- critical user journeys (registration, checkout, core workflow)
- data sensitivity tiers (public, internal, confidential, restricted)
- regulatory requirements (GDPR, CCPA, SOC2, HIPAA, PCI-DSS)

### Phase 2: Dimension Assessment

Grade the project across 12 dimensions. Each dimension produces a score from 0-100.

---

## Dimension 1: Security (Weight: 20%)

### What It Measures
How well the project defends against the full spectrum of security threats.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | All 24 security categories audited, no CRITICAL/HIGH findings, comprehensive controls |
| 80-89 | B | Most categories audited, no CRITICAL findings, minor HIGH findings with documented mitigations |
| 70-79 | C | Key categories covered, some HIGH findings exist but are non-exploitable or mitigated |
| 60-69 | D | Significant gaps in security coverage, CRITICAL or easily exploitable HIGH findings |
| 0-59 | F | Critical security vulnerabilities, missing fundamental controls |

### Assessment Method
Run the full `/launchify-security-audit` mental model across all 24 categories. For each category:
- Are checks present in the codebase?
- Are controls enforced server-side?
- Are controls tested?
- Are controls verified at deployment time?

Count confirmed findings by severity:
- Each CRITICAL finding: -15 points
- Each HIGH finding: -8 points
- Each MEDIUM finding: -3 points
- Each LOW finding: -1 point
- Each INFO finding: 0 points

Start at 100, subtract for findings. Floor at 0.

### Dimension Sub-Scores
- Secrets & Configuration: weight 15% of dimension
- Authentication: weight 15% of dimension
- Authorization: weight 15% of dimension
- API Security: weight 10% of dimension
- Web Security: weight 10% of dimension
- Infrastructure: weight 10% of dimension
- Dependencies: weight 5% of dimension
- AI/LLM/RAG: weight 5% of dimension (if applicable)
- Payments: weight 5% of dimension (if applicable)
- Other categories: remaining weight distributed

---

## Dimension 2: Reliability (Weight: 15%)

### What It Measures
How well the project handles failures, recovers from outages, and maintains availability.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Comprehensive error handling, retries, circuit breakers, health checks, graceful degradation |
| 80-89 | B | Good error handling, most edge cases covered, minor gaps |
| 70-79 | C | Basic error handling exists, significant gaps in recovery |
| 60-69 | D | Minimal error handling, frequent failure modes not addressed |
| 0-59 | F | No meaningful error handling, crashes on unexpected input |

### Assessment Method
Check for:
- Error handling on all critical paths (10 points)
- Retry logic with backoff on external calls (5 points)
- Circuit breakers on downstream dependencies (5 points)
- Health, readiness, liveness checks (5 points)
- Graceful degradation / fallback behavior (5 points)
- Rate limiting and throttling (5 points)
- Timeout handling on all external calls (5 points)
- Connection limits and resource bounds (5 points)
- Idempotency on non-idempotent operations (5 points)
- Dead-letter and poison-message handling (5 points)
- Graceful shutdown handling (5 points)
- Backpressure mechanisms (5 points)
- Request-size and response-size limits (5 points)
- Pagination on list endpoints (5 points)
- Cache invalidation strategy (5 points)

Each check: present and working = full points, partially present = half points, absent = 0 points.

Start at 0, add points. Cap at 100.

---

## Dimension 3: Code Quality (Weight: 10%)

### What It Measures
How clean, maintainable, and consistent the codebase is.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Clean architecture, consistent patterns, minimal dead code, comprehensive tests |
| 80-89 | B | Good quality, minor inconsistencies, reasonable test coverage |
| 70-79 | C | Acceptable quality, some duplication, inconsistent patterns |
| 60-69 | D | Poor quality, significant dead code, inconsistent architecture |
| 0-59 | F | Unmaintainable, no clear patterns, extensive technical debt |

### Assessment Method
Check for:
- Lint passes cleanly (10 points)
- Type checking passes cleanly (10 points)
- No dead code detected (10 points)
- No duplicate logic detected (10 points)
- Consistent patterns across the codebase (10 points)
- No AI-generated debris (10 points)
- Test coverage on critical paths (10 points)
- No commented-out code (5 points)
- No TODO/FIXME/HACK indicating unfinished work (5 points)
- No unnecessary complexity (10 points)
- No incomplete refactors (10 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 4: Testing (Weight: 10%)

### What It Measures
How well the project is tested and how confident we can be that changes don't break things.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Comprehensive unit, integration, and E2E tests; security regression tests; all passing |
| 80-89 | B | Good test coverage, most critical paths tested, tests passing |
| 70-79 | C | Basic tests exist, significant gaps in coverage |
| 60-69 | D | Minimal tests, many critical paths untested |
| 0-59 | F | No meaningful tests |

### Assessment Method
Check for:
- Unit tests exist and pass (20 points)
- Integration tests exist and pass (15 points)
- E2E tests exist for critical flows (10 points)
- Security regression tests exist (10 points)
- No permanently skipped tests (5 points)
- No flaky tests masked with retries (5 points)
- Tests assert behavior, not implementation details (10 points)
- Test data is realistic (5 points)
- No mock-only coverage that misses real behavior (5 points)
- No tests that pass only because security checks are disabled (5 points)
- Tests match production configuration (5 points)
- No tests for deleted behavior (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 5: Infrastructure (Weight: 10%)

### What It Measures
How well the infrastructure is configured, secured, and ready for production.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Fully configured, secured, monitored infrastructure with IaC |
| 80-89 | B | Good infrastructure, minor gaps in security or monitoring |
| 70-79 | C | Basic infrastructure exists, significant security or reliability gaps |
| 60-69 | D | Minimal infrastructure, critical security gaps |
| 0-59 | F | No production infrastructure configured |

### Assessment Method
Check for:
- Infrastructure-as-code exists (10 points)
- Network segmentation configured (5 points)
- IAM follows least privilege (10 points)
- Containers are hardened (10 points)
- Kubernetes manifests are secure (10 points)
- Secrets management is configured (10 points)
- Vulnerability scanning is in place (5 points)
- Server patching process exists (5 points)
- Deployment safety controls (10 points)
- Health checks configured (5 points)
- Resource limits set (5 points)
- Monitoring and alerting configured (5 points)
- Logging configured (5 points)
- Backup and restore tested (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 6: Deployment (Weight: 10%)

### What It Measures
How safe, automated, and reliable the deployment process is.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Automated, tested, reversible deployments with rollback |
| 80-89 | B | Automated deployments, rollback possible, minor gaps |
| 70-79 | C | Deployments work, limited automation, rollback uncertain |
| 60-69 | D | Manual deployments, no rollback, high deployment risk |
| 0-59 | F | No deployment process |

### Assessment Method
Check for:
- CI/CD pipeline exists (15 points)
- Automated testing in pipeline (10 points)
- Automated deployment (10 points)
- Rollback mechanism exists (10 points)
- Health checks gate deployment (5 points)
- Blue-green or canary deployment (5 points)
- Environment parity (5 points)
- Migration coordination (5 points)
- Deployment audit logging (5 points)
- Branch protection (5 points)
- Code review required (5 points)
- Artifact integrity verification (5 points)
- Environment protection rules (5 points)
- Deployment credentials follow least privilege (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 7: Monitoring & Observability (Weight: 5%)

### What It Measures
Whether you can detect, diagnose, and respond to problems in production.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Comprehensive monitoring, alerting, tracing, and incident response |
| 80-89 | B | Good monitoring, most critical signals covered |
| 70-79 | C | Basic monitoring, significant gaps |
| 60-69 | D | Minimal monitoring, blind spots in production |
| 0-59 | F | No monitoring |

### Assessment Method
Check for:
- Application performance monitoring (10 points)
- Error tracking (10 points)
- Security event monitoring (10 points)
- Infrastructure monitoring (10 points)
- Alerting configured (10 points)
- Audit logging for sensitive operations (10 points)
- Log retention policy (5 points)
- Distributed tracing (5 points)
- Custom business metrics (5 points)
- On-call and escalation (5 points)
- Incident response plan (10 points)
- Post-incident review process (5 points)
- Staging security parity (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 8: Feature Completeness (Weight: 10%)

### What It Measures
Whether the features that exist are complete, functional, and production-ready.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | All features complete with error handling, edge cases, and operational support |
| 80-89 | B | Most features complete, minor gaps |
| 70-79 | C | Core features work, significant gaps in edge cases or error handling |
| 60-69 | D | Features are partial, many missing requirements |
| 0-59 | F | Features are incomplete or broken |

### Assessment Method
Run the `/launchify-feature-audit` mental model. For each feature:
- Is the happy path complete? (1 point)
- Are error paths complete? (1 point)
- Is authorization enforced? (1 point)
- Is validation present? (1 point)
- Are loading/empty/error states handled? (1 point)
- Is retry/recovery behavior present? (1 point)
- Is monitoring/audit logging present? (1 point)
- Are tests present? (1 point)
- Is documentation present? (1 point)
- Is deployment configuration present? (1 point)

Score = (sum of points across all features) / (total possible points across all features) * 100.

---

## Dimension 9: Dependencies & Supply Chain (Weight: 5%)

### What It Measures
Whether dependencies are secure, up-to-date, and minimal.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | All dependencies current, no known vulnerabilities, minimal surface |
| 80-89 | B | Dependencies mostly current, no critical vulnerabilities |
| 70-79 | C | Some outdated dependencies, non-critical vulnerabilities |
| 60-69 | D | Multiple outdated or vulnerable dependencies |
| 0-59 | F | Critical vulnerable dependencies, no dependency management |

### Assessment Method
Check for:
- Lockfile exists and is consistent (10 points)
- No known critical vulnerabilities (20 points)
- No known high vulnerabilities (15 points)
- Dependencies are pinned (10 points)
- No unused dependencies (10 points)
- No duplicate packages (5 points)
- SBOM generated (5 points)
- Dependency scanning in CI (10 points)
- No malicious packages detected (10 points)
- No unpinned build actions (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 10: Documentation (Weight: 5%)

### What It Measures
Whether the project is documented well enough for someone to understand, operate, and troubleshoot it.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Comprehensive documentation covering setup, API, architecture, operations |
| 80-89 | B | Good documentation, minor gaps |
| 70-79 | C | Basic documentation, significant gaps |
| 60-69 | D | Minimal documentation |
| 0-59 | F | No documentation |

### Assessment Method
Check for:
- README with setup instructions (10 points)
- Environment variables documented (10 points)
- API documentation (10 points)
- Architecture description (10 points)
- Deployment instructions (10 points)
- Security documentation (10 points)
- Incident response documentation (5 points)
- Feature documentation (10 points)
- Contributing guidelines (5 points)
- Changelog (5 points)
- Documentation matches implementation (15 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 11: Privacy & Compliance (Weight: 5%)

### What It Measures
Whether the project handles data responsibly and meets regulatory requirements.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Full compliance with applicable regulations, strong privacy controls |
| 80-89 | B | Good privacy practices, minor compliance gaps |
| 70-79 | C | Basic privacy controls, compliance gaps |
| 60-69 | D | Weak privacy controls, significant compliance risk |
| 0-59 | F | No privacy controls, regulatory risk |

### Assessment Method
Check for:
- Encryption at rest (10 points)
- Encryption in transit (10 points)
- PII is identified and classified (10 points)
- Data retention policy exists (10 points)
- Deletion workflow exists (10 points)
- Consent management (5 points)
- Privacy policy exists and is accurate (10 points)
- Data masking in non-production (5 points)
- Audit logging for data access (10 points)
- No PII in logs (10 points)
- Third-party data sharing is documented (5 points)
- No sensitive data in client-side storage (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Dimension 12: Operational Readiness (Weight: 5%)

### What It Measures
Whether the team can operate, debug, and support the system in production.

### Scoring Criteria

| Score Range | Grade | Meaning |
|---|---|---|
| 90-100 | A | Runbooks, on-call, incident response, support workflows, capacity planning |
| 80-89 | B | Good operational readiness, minor gaps |
| 70-79 | C | Basic operational support, significant gaps |
| 60-69 | D | Minimal operational readiness |
| 0-59 | F | No operational readiness |

### Assessment Method
Check for:
- Incident response plan (10 points)
- Runbooks for common scenarios (10 points)
- On-call rotation (5 points)
- Escalation paths (5 points)
- Support workflows (10 points)
- Admin dashboard or tooling (10 points)
- Feature flags for safe rollouts (5 points)
- Rollback procedures (10 points)
- Capacity planning data (5 points)
- Cost monitoring (5 points)
- Post-incident review process (5 points)
- Customer communication process (5 points)
- Regulatory notification process (5 points)

Each check: present = full points, partially = half, absent = 0. Start at 0, add points, cap at 100.

---

## Overall Grade Calculation

### Weighted Score

```
Overall = (Security * 0.20) +
          (Reliability * 0.15) +
          (Code Quality * 0.10) +
          (Testing * 0.10) +
          (Infrastructure * 0.10) +
          (Deployment * 0.10) +
          (Monitoring * 0.05) +
          (Feature Completeness * 0.10) +
          (Dependencies * 0.05) +
          (Documentation * 0.05) +
          (Privacy * 0.05) +
          (Operational Readiness * 0.05)
```

### Letter Grade

| Score | Grade | Meaning |
|---|---|---|
| 93-100 | A+ | Exceptional — production-ready with confidence |
| 90-92 | A | Excellent — production-ready |
| 87-89 | B+ | Very Good — nearly production-ready |
| 83-86 | B | Good — production-ready with minor reservations |
| 80-82 | B- | Above Average — production-ready with noted gaps |
| 77-79 | C+ | Average — production-viable with important gaps to close |
| 73-76 | C | Below Average — significant work needed |
| 70-72 | C- | Poor — not production-ready |
| 60-69 | D | Very Poor — substantial production readiness gaps |
| 0-59 | F | Failing — not suitable for production |

### Hard Fail Conditions

Regardless of overall score, the project receives an automatic **F** if ANY of the following are true:
- Any CRITICAL security vulnerability is confirmed and unmitigated
- No authentication on sensitive endpoints
- No authorization on multi-tenant data
- Database publicly accessible without authentication
- Secrets hardcoded in source code and accessible to untrusted parties
- No backups or restore capability
- No rollback mechanism

---

## Output Format

### Summary Report (`docs/launchify/production-grade.md`)

```markdown
# Launchify Production Grade Report

**Date:** {date}
**Project:** {project name}
**Overall Grade:** {letter grade} ({score}/100)

## Dimension Scores

| Dimension | Score | Grade | Weight | Weighted |
|---|---|---|---|---|
| Security | {score} | {grade} | 20% | {weighted} |
| Reliability | {score} | {grade} | 15% | {weighted} |
| Code Quality | {score} | {grade} | 10% | {weighted} |
| Testing | {score} | {grade} | 10% | {weighted} |
| Infrastructure | {score} | {grade} | 10% | {weighted} |
| Deployment | {score} | {grade} | 10% | {weighted} |
| Monitoring | {score} | {grade} | 5% | {weighted} |
| Feature Completeness | {score} | {grade} | 10% | {weighted} |
| Dependencies | {score} | {grade} | 5% | {weighted} |
| Documentation | {score} | {grade} | 5% | {weighted} |
| Privacy | {score} | {grade} | 5% | {weighted} |
| Operational Readiness | {score} | {grade} | 5% | {weighted} |

## Hard Fail Conditions
- {list any triggered hard fail conditions}

## Critical Findings
- {findings that must be resolved before production}

## Priority Remediation Path
1. {highest priority item}
2. {next priority}
...

## Dimension Details
{per-dimension breakdown with specific findings}
```

### CSV Report (`docs/launchify/production-grade.csv`)

| Column | Description |
|---|---|
| Dimension | Dimension name |
| Score | 0-100 score |
| Grade | Letter grade |
| Weight | Percentage weight |
| Weighted Score | Score * Weight |
| Finding Count | Number of findings in this dimension |
| Critical Findings | Number of CRITICAL findings |
| High Findings | Number of HIGH findings |
| Recommendation | Top recommendation for improvement |

---

## Important Rules

1. This command does NOT modify code. It is read-only.
2. Every score must be backed by evidence from the codebase.
3. Do not inflate scores — be honest about gaps.
4. A project can have a high score and still have critical findings that must be fixed.
5. The grade is a snapshot in time — it reflects the current state of the repository.
6. When dimensions are not applicable (e.g., no payments), weight is redistributed to applicable dimensions proportionally.
7. Hard fail conditions override the score — a project with a CRITICAL vulnerability cannot be production-ready regardless of other dimensions.
