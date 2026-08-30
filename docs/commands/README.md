# Command Reference

Launchify provides 58 commands across 6 command groups. Every command is available on all three platforms (Claude Code, OpenCode, Codex) with identical behavior.

---

## 🔒 Security Commands

### `/launchify-security`

**Full security audit and remediation.**

Runs all 24 security categories. For each category:
1. Reads the category definition from `.launchify/categories/{category}.md`
2. Performs checks defined in that category
3. Traces actual code paths, infrastructure paths, and deployment paths
4. Produces evidence-backed findings
5. Validates each finding and removes false positives
6. Ranks severity (CRITICAL, HIGH, MEDIUM, LOW, INFO)
7. Determines exploitability
8. Fixes issues that can safely be fixed
9. Adds or updates security regression tests
10. Runs relevant tests
11. Re-audits modified areas
12. Verifies that vulnerabilities are actually resolved
13. Generates final reports in `docs/launchify/`

**Output:** `docs/launchify/security-report.csv`, `docs/launchify/security-summary.md`, `docs/launchify/security-fixes.md`

---

### `/launchify-security-audit`

**Full security audit only — no code changes.**

Same as `/launchify-security` but does NOT modify production code, infrastructure, deployment configuration, or application behavior.

**Output:** `docs/launchify/security-report.csv`, `docs/launchify/security-summary.md`

---

### `/launchify-security-secrets`

**Audit and remediate secrets & configuration security.**

Checks: exposed credentials, hardcoded secrets, Git history leaks, public `.env` files, secrets in bundles/source maps/build artifacts/container layers/infrastructure outputs/CI-CD secrets, default credentials, verbose production errors, configuration drift.

**Output:** Report in `docs/launchify/security-report.csv`

---

### `/launchify-security-secrets-audit`

**Audit only — no modifications.** Same checks. Does not modify code.

---

### `/launchify-security-authentication`

**Audit and remediate authentication & identity security.**

Checks: weak passwords, broken reset flows, session fixation, JWT issues, OAuth/SSO misconfiguration, missing MFA, privilege escalation, account enumeration, session management.

---

### `/launchify-security-authentication-audit`

**Audit only — no modifications.**

---

### `/launchify-security-authorization`

**Audit and remediate authorization & access control.**

Checks: IDOR, BOLA, cross-user/tenant access, missing ownership checks, unprotected admin routes, mass assignment, excessive permissions, role escalation, missing resource/field-level authorization.

---

### `/launchify-security-authorization-audit`

**Audit only — no modifications.**

---

### `/launchify-security-database`

**Audit and remediate database & data-access security.**

Checks: SQL/NoSQL injection, unsafe queries, missing parameterization, open permissions, public exposure, missing encryption, sensitive data exposure, unbounded queries, unsafe migrations, missing tenant isolation.

---

### `/launchify-security-database-audit`

**Audit only — no modifications.**

---

### `/launchify-security-api`

**Audit and remediate API security.**

Checks: unsecured endpoints, missing auth, broken object-level authorization, missing validation, mass assignment, excessive data exposure, missing rate limits, GraphQL vulnerabilities, legacy endpoints, missing idempotency.

---

### `/launchify-security-api-audit`

**Audit only — no modifications.**

---

### `/launchify-security-web`

**Audit and remediate web application security.**

Checks: XSS, CSRF, SSRF, XXE, command injection, path traversal, open redirects, insecure file uploads, missing security headers, CORS misconfiguration, cookie security, clickjacking, prototype pollution.

---

### `/launchify-security-web-audit`

**Audit only — no modifications.**

---

### `/launchify-security-frontend`

**Audit and remediate frontend security.**

Checks: client-side security reliance, frontend secrets, exposed source maps, unsafe localStorage, third-party script risks, DOM-based XSS, prototype pollution, insecure postMessage, exposed feature flags, debug tooling in production.

---

### `/launchify-security-frontend-audit`

**Audit only — no modifications.**

---

### `/launchify-security-cloud`

**Audit and remediate cloud security.**

Checks: overprivileged IAM, wildcard policies, public storage, missing encryption, network misconfiguration, metadata endpoint exposure, missing audit logging, excessive cross-account access, long-lived credentials.

---

### `/launchify-security-cloud-audit`

**Audit only — no modifications.**

---

### `/launchify-security-infrastructure`

**Audit and remediate infrastructure security.**

Checks: network segmentation, container security, Kubernetes RBAC, WAF protections, vulnerability scanning, server patching, infrastructure secrets exposure, deployment safety, image provenance.

---

### `/launchify-security-infrastructure-audit`

**Audit only — no modifications.**

---

### `/launchify-security-deployment`

**Audit and remediate deployment security.**

Checks: insecure defaults, missing rollback, missing health checks, configuration drift, environment parity, artifact integrity, mutable images, excessive deployment credentials, direct production access.

---

### `/launchify-security-deployment-audit`

**Audit only — no modifications.**

---

### `/launchify-security-dependencies`

**Audit and remediate dependency & supply-chain security.**

Checks: vulnerable packages, malicious packages, unpinned dependencies, missing lockfiles, typosquatting, install-script risk, missing SBOM, dependency scanning.

---

### `/launchify-security-dependencies-audit`

**Audit only — no modifications.**

---

### `/launchify-security-cicd`

**Audit and remediate CI/CD security.**

Checks: exposed CI secrets, untrusted actions, unpinned build actions, excessive build permissions, command injection in CI variables, missing branch protection, missing artifact signing, fork PR secret exposure.

---

### `/launchify-security-cicd-audit`

**Audit only — no modifications.**

---

### `/launchify-security-logging`

**Audit and remediate logging security.**

Checks: sensitive data in logs, API keys in logs, PII in logs, missing audit logs, exposed logs, missing log retention, missing log integrity, missing time synchronization.

---

### `/launchify-security-logging-audit`

**Audit only — no modifications.**

---

### `/launchify-security-monitoring`

**Audit and remediate monitoring gaps.**

Checks: missing security monitoring, missing anomaly detection, missing alerting, missing authentication monitoring, missing payment-abuse monitoring, missing AI abuse monitoring, missing data-exfiltration monitoring.

---

### `/launchify-security-monitoring-audit`

**Audit only — no modifications.**

---

### `/launchify-security-ai`

**Audit and remediate AI & LLM security.**

Checks: prompt injection, system prompt leakage, jailbreaks, unsafe AI output, missing output validation, excessive AI permissions, sensitive data in prompts, model endpoint exposure, model abuse, unbounded token usage, missing human approval gates.

---

### `/launchify-security-ai-audit`

**Audit only — no modifications.**

---

### `/launchify-security-rag`

**Audit and remediate RAG & vector security.**

Checks: exposed vector databases, missing retrieval authorization, cross-tenant retrieval, vector poisoning, document-based prompt injection, deleted documents remaining retrievable, missing tenant-aware indexing, unsafe ingestion.

---

### `/launchify-security-rag-audit`

**Audit only — no modifications.**

---

### `/launchify-security-agents`

**Audit and remediate AI agent security.**

Checks: excessive tool permissions, unrestricted filesystem/database access, destructive actions without approval, tool-output injection, agent memory poisoning, missing action auditing, agents able to deploy/modify infrastructure, missing rollback capability.

---

### `/launchify-security-agents-audit`

**Audit only — no modifications.**

---

### `/launchify-security-payments`

**Audit and remediate payment & business-logic security.**

Checks: price manipulation, coupon abuse, refund abuse, subscription bypass, unsigned webhooks, webhook replay, duplicate processing, race conditions, client-controlled entitlement state, missing payment audit logs.

---

### `/launchify-security-payments-audit`

**Audit only — no modifications.**

---

### `/launchify-security-privacy`

**Audit and remediate data protection & privacy.**

Checks: PII overcollection, missing encryption, missing retention policies, missing deletion workflows, privacy-policy mismatch, sensitive data in logs/client storage/AI providers, missing consent management, missing data classification.

---

### `/launchify-security-privacy-audit`

**Audit only — no modifications.**

---

### `/launchify-security-reliability`

**Audit and remediate reliability & recovery.**

Checks: missing backups, untested restoration, missing rate limiting, infinite retries, resource exhaustion, missing circuit breakers, missing health checks, unbounded queries, missing idempotency, missing graceful degradation.

---

### `/launchify-security-reliability-audit`

**Audit only — no modifications.**

---

### `/launchify-security-code-quality`

**Audit and remediate code quality & security process.**

Checks: unreviewed code, missing security review, missing threat modeling, missing SAST/DAST, dead vulnerable code, debug code, missing security regression tests, missing vulnerability remediation process, missing staging security parity.

---

### `/launchify-security-code-quality-audit`

**Audit only — no modifications.**

---

### `/launchify-security-business-logic`

**Audit and remediate business logic security.**

Checks: workflow bypasses, step skipping, state machine manipulation, race conditions in business flows, missing server-side validation, missing abuse prevention, missing entitlement enforcement, entitlement bypass through API manipulation.

---

### `/launchify-security-business-logic-audit`

**Audit only — no modifications.**

---

### `/launchify-security-incident-response`

**Audit and remediate incident response gaps.**

Checks: no incident response plan, missing breach notification, missing escalation paths, missing incident ownership, missing runbooks, missing forensic preservation, missing post-incident review, missing tabletop exercises.

---

### `/launchify-security-incident-response-audit`

**Audit only — no modifications.**

---

### `/launchify-security-feature-readiness`

**Audit and remediate feature readiness.**

Checks: missing error handling, missing authorization on feature endpoints, missing tenant isolation, missing retry behavior, missing monitoring, missing documentation, missing accessibility, missing tests, missing deployment configuration.

---

### `/launchify-security-feature-readiness-audit`

**Audit only — no modifications.**

---

## 🧹 Cleanup Commands

### `/launchify-cleanup`

**Repository cleanup and simplification.**

Performs a repository-wide cleanup, simplification, deduplication, and maintainability pass. Classifies each finding as:
- `SAFE_TO_REMOVE` — dead code, unused imports, empty files
- `SAFE_TO_SIMPLIFY` — duplicated logic, over-abstracted patterns
- `REVIEW_REQUIRED` — needs human judgment
- `LIKELY_INTENTIONAL` — may serve a hidden purpose
- `DO_NOT_TOUCH` — critical infrastructure, complex business logic

Makes changes incrementally, running tests after each change.

**Output:** `docs/launchify/cleanup-report.csv`, `docs/launchify/cleanup-summary.md`

---

### `/launchify-cleanup-audit`

**Cleanup analysis only — no modifications.**

Same analysis. Does not modify production code.

**Output:** `docs/launchify/cleanup-report.csv`, `docs/launchify/cleanup-summary.md`

---

## 🧩 Feature Commands

### `/launchify-feature-audit`

**Audit all features for completeness, security, and production readiness.**

Discovers all features in the repository. Traces each feature's complete lifecycle: entry points, data flow, API endpoints, database models, UI components, tests, and deployment configuration.

Classifies each feature as:
- Complete — production-ready, all requirements met
- Underbuilt — missing important requirements
- Overbuilt — complexity not justified by usage
- Partially implemented — partially working
- Broken — known issues, failing, or non-functional
- Insecure — has security vulnerabilities
- Unreliable — no error handling, no retry, no fallback
- Inconsistent — behavior varies across environments
- Poorly integrated — disconnected from main flows
- Missing edge cases — happy path only
- Missing operational support — no monitoring, logging, alerting
- Abandoned — no recent activity, likely unused

**Output:** `docs/launchify/feature-report.csv`, `docs/launchify/feature-summary.md`

---

### `/launchify-feature-audit-fix`

**Feature audit and remediation.**

Runs the feature audit, then safely remediates confirmed feature issues. Only modifies features when:
1. The intended behavior is clear
2. The change is supported by repository evidence
3. The change can be implemented without inventing product policy
4. The change can be verified

---

## ✅ Verification Commands

### `/launchify-verify`

**Verify changes and production readiness.**

Runs:
- Build verification (all build targets)
- Lint (all linters configured in the project)
- Type checking (all TypeScript, mypy, or equivalent)
- Unit tests
- Integration tests
- End-to-end tests
- Security regression tests
- Dependency integrity (lockfile consistency)
- Route availability (all defined routes exist)
- API contracts (request/response schemas match)
- Public exports (no broken exports)
- Configuration references (all config keys referenced)
- Infrastructure validation
- Deployment manifests
- Container configuration
- Kubernetes manifests
- Infrastructure-as-code validation
- Migration consistency
- Environment-variable consistency
- Observability configuration
- Rollback readiness

**Output:** `docs/launchify/verification.md`

---

### `/launchify-report`

**Generate or refresh reports.**

Generates or refreshes Launchify reports based on the latest analysis without modifying production code. Use after running audit commands to get fresh reports, or to regenerate reports after manual changes.

---

## 🎓 Production Grading Commands

### `/launchify-production-grade`

**Grade the project on production readiness.**

Scores the project across 12 dimensions:

| Dimension | Weight |
|---|---|
| Security | 20% |
| Reliability | 15% |
| Code Quality | 10% |
| Testing | 10% |
| Infrastructure | 10% |
| Deployment | 10% |
| Feature Completeness | 10% |
| Monitoring | 5% |
| Dependencies | 5% |
| Documentation | 5% |
| Privacy | 5% |
| Operational Readiness | 5% |

For each dimension:
1. Score 0-100 based on evidence from the codebase
2. Identify findings (critical, high, medium, low)
3. Provide recommendations

Produces:
- Letter grade (A+ through F)
- Weighted overall score
- Per-dimension breakdowns
- Prioritized remediation path

**Hard fail conditions** (automatic F regardless of other scores):
- Any CRITICAL security vulnerability
- Missing authentication on sensitive endpoints
- Missing authorization on multi-tenant data
- Publicly accessible database
- Hardcoded secrets
- No backups
- No rollback mechanism

**This command does NOT modify code. It is read-only.**

**Output:** `docs/launchify/production-grade.md`, `docs/launchify/production-grade.csv`

---

### `/launchify-production-branch`

**Analyze branch merge readiness.**

Identifies the current branch and target branch (default: main). Computes the diff. For every change:
1. Categorizes the change (feature, endpoint, migration, config, infrastructure, dependency)
2. Evaluates completeness, security, reliability, testing, data integrity, deployment requirements, documentation
3. Classifies as:
   - `MERGE_READY` — safe to merge
   - `MERGE_WITH_CAUTION` — mergeable but needs attention
   - `NEEDS_FIXES` — must fix before merge
   - `NEEDS_REVIEW` — needs human review
   - `HOLD` — do not merge yet
   - `DEV_ONLY` — keep on dev branch
   - `REVERT` — should be reverted
4. Assigns risk level per change
5. Checks dependencies between changes
6. Produces overall verdict:
   - `MERGE_NOW` — all changes safe
   - `MERGE_WITH_ORDER` — merge in specific order
   - `PARTIAL_MERGE` — some changes safe, some not
   - `HOLD_MERGE` — nothing is safe to merge
   - `REVERT_AND_MERGE` — revert problematic changes, then merge

**This command does NOT merge anything. It is read-only.**

**Output:** `docs/launchify/production-branch.md`, `docs/launchify/production-branch.csv`
