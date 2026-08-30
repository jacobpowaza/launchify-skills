# Launchify — Claude Code Skill

**Name:** launchify
**Description:** Production-readiness skill suite for security auditing, cleanup, feature auditing, and remediation. Triggers on `/launchify-*` commands.

---

## Trigger

This skill activates when the user types any command starting with `/launchify-`.

---

## Canonical Specification

This skill implements the Launchify canonical specification located at `.launchify/spec.md`.

Before performing any action, read the following files in order:

1. `.launchify/spec.md` — canonical specification and command definitions
2. `.launchify/safety.md` — safety and production safety rules
3. `.launchify/remediation.md` — remediation rules (for modifying commands)
4. `.launchify/cleanup.md` — cleanup rules (for cleanup commands)
5. `.launchify/verification.md` — verification rules (for verify command)
6. `.launchify/feature-audit.md` — feature audit rules (for feature commands)
7. `.launchify/production-grade.md` — production grading rules (for grade command)
8. `.launchify/production-branch.md` — branch readiness rules (for branch command)

For security commands, also read the relevant category file from `.launchify/categories/`.
For infrastructure commands, also read `.launchify/checks/infrastructure.md`.

---

## Commands

### `/launchify-security`

**Full security audit and remediation.**

1. Read `.launchify/spec.md` to understand the full command specification
2. Read `.launchify/safety.md` for safety rules
3. Read `.launchify/remediation.md` for remediation rules
4. Establish a repository model by inspecting the project structure, frameworks, languages, databases, authentication, authorization, API definitions, frontend, infrastructure, CI/CD, and deployment
5. For each of the 24 security categories (secrets, authentication, authorization, database, api, web, frontend, cloud, infrastructure, deployment, dependencies, cicd, logging, monitoring, ai, rag, agents, payments, privacy, reliability, code-quality, business-logic, incident-response, feature-readiness):
   a. Read the category definition from `.launchify/categories/{category}.md`
   b. Perform the checks defined in that category
   c. Trace actual code paths, infrastructure paths, and deployment paths
   d. Produce evidence-backed findings
6. Validate each finding and remove false positives
7. Rank severity (CRITICAL, HIGH, MEDIUM, LOW, INFO)
8. Determine exploitability
9. Fix issues that can safely be fixed following remediation rules
10. Add or update security regression tests
11. Run relevant tests
12. Re-audit modified areas
13. Verify that vulnerabilities are actually resolved
14. Generate final reports in `docs/launchify/` using the schemas from `.launchify/schemas/`

### `/launchify-security-audit`

**Full security audit only — no modifications.**

Perform the exact same assessment as `/launchify-security`, but DO NOT modify production code, infrastructure, deployment configuration, or application behavior.

Generate reports in `docs/launchify/`.

### `/launchify-security-secrets`

**Audit and remediate secrets & configuration security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/secrets.md`
3. Establish repository model focused on secrets and configuration
4. Check: exposed credentials, hardcoded secrets, Git history leaks, public .env files, secrets in bundles/source maps/build artifacts/container layers/infrastructure outputs/CI-CD secrets, default credentials, verbose production errors, configuration drift
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports in `docs/launchify/`

### `/launchify-security-secrets-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-authentication`

**Audit and remediate authentication & identity security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/authentication.md`
3. Establish repository model focused on authentication
4. Check: weak passwords, broken reset flows, session fixation, JWT issues, OAuth/SSO misconfiguration, missing MFA, privilege escalation, account enumeration, session management
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-authentication-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-authorization`

**Audit and remediate authorization & access control.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/authorization.md`
3. Establish repository model focused on authorization
4. Check: IDOR, BOLA, cross-user/tenant access, missing ownership checks, unprotected admin routes, mass assignment, excessive permissions, role escalation, missing resource/field-level authorization
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-authorization-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-database`

**Audit and remediate database & data-access security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/database.md`
3. Establish repository model focused on database
4. Check: SQL/NoSQL injection, unsafe queries, missing parameterization, open permissions, public exposure, missing encryption, sensitive data exposure, unbounded queries, unsafe migrations, missing tenant isolation
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-database-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-api`

**Audit and remediate API security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/api.md`
3. Establish repository model focused on API endpoints
4. Check: unsecured endpoints, missing auth, broken object-level authorization, missing validation, mass assignment, excessive data exposure, missing rate limits, GraphQL vulnerabilities, legacy endpoints, missing idempotency
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-api-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-web`

**Audit and remediate web application security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/web.md`
3. Establish repository model focused on web security
4. Check: XSS, CSRF, SSRF, XXE, command injection, path traversal, open redirects, insecure file uploads, missing security headers, CORS misconfiguration, cookie security, clickjacking, prototype pollution
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-web-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-frontend`

**Audit and remediate frontend security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/frontend.md`
3. Establish repository model focused on frontend
4. Check: client-side security reliance, frontend secrets, exposed source maps, unsafe localStorage, third-party script risks, DOM-based XSS, prototype pollution, insecure postMessage, exposed feature flags, debug tooling in production
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-frontend-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-cloud`

**Audit and remediate cloud security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/cloud.md`
3. Establish repository model focused on cloud
4. Check: overprivileged IAM, wildcard policies, public storage, missing encryption, network misconfiguration, metadata endpoint exposure, missing audit logging, excessive cross-account access, long-lived credentials
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-cloud-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-infrastructure`

**Audit and remediate infrastructure security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/infrastructure.md` and `.launchify/checks/infrastructure.md`
3. Establish repository model focused on infrastructure
4. Check: network segmentation, container security, Kubernetes RBAC, WAF protections, vulnerability scanning, server patching, infrastructure secrets exposure, deployment safety, image provenance
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-infrastructure-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-deployment`

**Audit and remediate deployment security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/deployment.md`
3. Establish repository model focused on deployment
4. Check: insecure defaults, missing rollback, missing health checks, configuration drift, environment parity, artifact integrity, mutable images, excessive deployment credentials, direct production access
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-deployment-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-dependencies`

**Audit and remediate dependency & supply-chain security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/dependencies.md`
3. Establish repository model focused on dependencies
4. Check: vulnerable packages, malicious packages, unpinned dependencies, missing lockfiles, typosquatting, install-script risk, missing SBOM, dependency scanning
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-dependencies-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-cicd`

**Audit and remediate CI/CD security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/cicd.md`
3. Establish repository model focused on CI/CD
4. Check: exposed CI secrets, untrusted actions, unpinned build actions, excessive build permissions, command injection in CI variables, missing branch protection, missing artifact signing, fork PR secret exposure
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-cicd-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-logging`

**Audit and remediate logging security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/logging.md`
3. Establish repository model focused on logging
4. Check: sensitive data in logs, API keys in logs, PII in logs, missing audit logs, exposed logs, missing log retention, missing log integrity, missing time synchronization
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-logging-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-monitoring`

**Audit and remediate monitoring gaps.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/monitoring.md`
3. Establish repository model focused on monitoring
4. Check: missing security monitoring, missing anomaly detection, missing alerting, missing authentication monitoring, missing payment-abuse monitoring, missing AI abuse monitoring, missing data-exfiltration monitoring
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-monitoring-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-ai`

**Audit and remediate AI & LLM security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/ai.md`
3. Establish repository model focused on AI/LLM integrations
4. Check: prompt injection, system prompt leakage, jailbreaks, unsafe AI output, missing output validation, excessive AI permissions, sensitive data in prompts, model endpoint exposure, model abuse, unbounded token usage, missing human approval gates
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-ai-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-rag`

**Audit and remediate RAG & vector security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/rag.md`
3. Establish repository model focused on RAG pipeline
4. Check: exposed vector databases, missing retrieval authorization, cross-tenant retrieval, vector poisoning, document-based prompt injection, deleted documents remaining retrievable, missing tenant-aware indexing, unsafe ingestion
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-rag-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-agents`

**Audit and remediate AI agent security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/agents.md`
3. Establish repository model focused on AI agents
4. Check: excessive tool permissions, unrestricted filesystem/database access, destructive actions without approval, tool-output injection, agent memory poisoning, missing action auditing, agents able to deploy/modify infrastructure, missing rollback capability
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-agents-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-payments`

**Audit and remediate payment & business-logic security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/payments.md`
3. Establish repository model focused on payments
4. Check: price manipulation, coupon abuse, refund abuse, subscription bypass, unsigned webhooks, webhook replay, duplicate processing, race conditions, client-controlled entitlement state, missing payment audit logs
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-payments-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-privacy`

**Audit and remediate data protection & privacy.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/privacy.md`
3. Establish repository model focused on privacy
4. Check: PII overcollection, missing encryption, missing retention policies, missing deletion workflows, privacy-policy mismatch, sensitive data in logs/client storage/AI providers, missing consent management, missing data classification
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-privacy-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-reliability`

**Audit and remediate reliability & recovery.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/reliability.md`
3. Establish repository model focused on reliability
4. Check: missing backups, untested restoration, missing rate limiting, infinite retries, resource exhaustion, missing circuit breakers, missing health checks, unbounded queries, missing idempotency, missing graceful degradation
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-reliability-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-code-quality`

**Audit and remediate code quality & security process.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/code-quality.md`
3. Establish repository model focused on code quality
4. Check: unreviewed code, missing security review, missing threat modeling, missing SAST/DAST, dead vulnerable code, debug code, missing security regression tests, missing vulnerability remediation process, missing staging security parity
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-code-quality-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-business-logic`

**Audit and remediate business logic security.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/business-logic.md`
3. Establish repository model focused on business logic
4. Check: workflow bypasses, step skipping, state machine manipulation, race conditions in business flows, missing server-side validation, missing abuse prevention, missing entitlement enforcement, entitlement bypass through API manipulation
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-business-logic-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-incident-response`

**Audit and remediate incident response gaps.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/incident-response.md`
3. Establish repository model focused on incident response
4. Check: no incident response plan, missing breach notification, missing escalation paths, missing incident ownership, missing runbooks, missing forensic preservation, missing post-incident review, missing tabletop exercises
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-incident-response-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-security-feature-readiness`

**Audit and remediate feature readiness.**

1. Read `.launchify/safety.md`, `.launchify/remediation.md`
2. Read `.launchify/categories/feature-readiness.md`
3. Establish repository model focused on features
4. Check: missing error handling, missing authorization on feature endpoints, missing tenant isolation, missing retry behavior, missing monitoring, missing documentation, missing accessibility, missing tests, missing deployment configuration
5. Produce evidence-backed findings, fix issues that can safely be fixed
6. Run tests, generate reports

### `/launchify-security-feature-readiness-audit`

**Audit only — no modifications.** Same checks as above. Do not modify code.

### `/launchify-cleanup`

**Repository cleanup and simplification.**

1. Read `.launchify/spec.md`
2. Read `.launchify/safety.md`
3. Read `.launchify/cleanup.md`
4. Understand the project before deleting anything
5. Identify dead code, duplicate logic, unused components, unnecessary complexity, AI-generated debris, dependency issues, configuration issues, architectural inconsistencies, incomplete refactors, test issues, and documentation issues
6. Classify each finding as SAFE_TO_REMOVE, SAFE_TO_SIMPLIFY, REVIEW_REQUIRED, LIKELY_INTENTIONAL, or DO_NOT_TOUCH
7. Make changes incrementally, running tests after each change
8. Generate reports in `docs/launchify/` using the cleanup CSV schema

### `/launchify-cleanup-audit`

**Cleanup analysis only — no modifications.**

Perform the same analysis as `/launchify-cleanup` but make no changes. Generate the cleanup report.

### `/launchify-feature-audit`

**Audit all features for completeness, security, and production readiness.**

1. Read `.launchify/spec.md`
2. Read `.launchify/safety.md`
3. Read `.launchify/feature-audit.md`
4. Establish a repository model
5. Discover all features
6. Trace each feature's complete lifecycle
7. Classify each feature (COMPLETE, UNDERBUILT, OVERBUILT, PARTIALLY_IMPLEMENTED, BROKEN, INSECURE, UNRELIABLE, UNUSED, DUPLICATED, ABANDONED, MISSING_REQUIREMENTS, REVIEW_REQUIRED)
8. Generate reports in `docs/launchify/` using the feature CSV schema

### `/launchify-feature-audit-fix`

**Feature audit and remediation.**

Run the feature audit, then safely remediate confirmed feature issues. Only modify features when the intended behavior is clear and the change can be verified. After remediation, update tests, run verification, and re-audit modified features.

### `/launchify-verify`

**Verify changes and production readiness.**

1. Read `.launchify/spec.md`
2. Read `.launchify/verification.md`
3. Run builds, lint, type checking, unit tests, integration tests, and relevant end-to-end tests
4. Check dependency integrity, route availability, API contracts, public exports
5. Validate configuration references, infrastructure, deployment manifests
6. Detect regressions and report findings
7. Re-run appropriate Launchify checks against modified areas

### `/launchify-report`

**Generate or refresh reports.**

Generate or refresh Launchify reports based on the latest analysis without modifying production code. Read the latest findings and produce the appropriate CSV and summary reports in `docs/launchify/`.

### `/launchify-production-grade`

**Grade the project on production readiness.**

1. Read `.launchify/spec.md`
2. Read `.launchify/safety.md`
3. Read `.launchify/production-grade.md`
4. Establish a complete repository model
5. Grade the project across 12 dimensions:
   - Security (20%): Run the full security audit mental model across all 24 categories
   - Reliability (15%): Check error handling, retries, circuit breakers, health checks, graceful degradation
   - Code Quality (10%): Check lint, type checking, dead code, duplication, consistency, AI debris
   - Testing (10%): Check unit, integration, E2E, security regression tests
   - Infrastructure (10%): Check IaC, IAM, containers, Kubernetes, secrets, scanning
   - Deployment (10%): Check CI/CD, rollback, health gates, environment parity
   - Feature Completeness (10%): Trace each feature's lifecycle for completeness
   - Monitoring (5%): Check APM, error tracking, security monitoring, alerting
   - Dependencies (5%): Check lockfile, vulnerabilities, pinning, SBOM
   - Documentation (5%): Check README, API docs, architecture, operations docs
   - Privacy (5%): Check encryption, PII handling, retention, consent
   - Operational Readiness (5%): Check runbooks, on-call, incident response, support workflows
6. Score each dimension 0-100 with evidence
7. Calculate weighted overall score
8. Apply hard fail conditions (any CRITICAL vulnerability = automatic F)
9. Produce letter grade (A+ through F)
10. Generate `docs/launchify/production-grade.md` and `docs/launchify/production-grade.csv`
11. Do NOT modify code — this is read-only

### `/launchify-production-branch`

**Analyze branch merge readiness.**

1. Read `.launchify/spec.md`
2. Read `.launchify/safety.md`
3. Read `.launchify/production-branch.md`
4. Identify the current branch and target branch (default: main)
5. Compute the diff between the branch and the target
6. Categorize every change (feature, page, component, endpoint, model, migration, config, infrastructure, dependency, refactor, fix, security, test, documentation, cleanup)
7. For each change, evaluate:
   - Completeness (happy path, error paths, edge cases, loading/empty/error states)
   - Security (authentication, authorization, input validation, secrets, dependencies)
   - Reliability (error handling, retries, timeouts, rate limiting, idempotency)
   - Testing (unit, integration, E2E, security regression tests)
   - Data Integrity (migration reversibility, rollback, dry-run, idempotency)
   - Deployment (coordination, env vars, secrets, feature flags, deployment order)
   - Documentation (API docs, env vars, features, deployment steps)
8. Classify each change (MERGE_READY, MERGE_WITH_CAUTION, NEEDS_FIXES, NEEDS_REVIEW, HOLD, DEV_ONLY, REVERT)
9. Assign risk level per change (NONE, LOW, MEDIUM, HIGH, CRITICAL)
10. Check dependencies between changes
11. Produce overall verdict (MERGE_NOW, MERGE_WITH_ORDER, PARTIAL_MERGE, HOLD_MERGE, REVERT_AND_MERGE)
12. Generate `docs/launchify/production-branch.md` and `docs/launchify/production-branch.csv`
13. Do NOT merge anything — this is read-only

---

## Repository Understanding

Before any action, establish a repository model by inspecting:
- repository layout and workspace structure
- languages, frameworks, package managers
- build tooling, runtime entrypoints
- database, migration system
- authentication, authorization
- API definitions, frontend applications
- background workers, queues, scheduled jobs
- cloud configuration, infrastructure-as-code
- CI/CD, deployment targets
- containerization, Kubernetes
- network topology, IAM definitions
- secret-management systems
- AI providers, model calls, RAG pipeline
- payment providers, external integrations
- tests, feature flags, documentation

---

## Reporting

Store all output in `docs/launchify/` unless the project has an established report directory.

Generate only reports relevant to the commands that ran:
- `docs/launchify/security-report.csv`
- `docs/launchify/security-summary.md`
- `docs/launchify/security-fixes.md`
- `docs/launchify/cleanup-report.csv`
- `docs/launchify/cleanup-summary.md`
- `docs/launchify/feature-report.csv`
- `docs/launchify/feature-summary.md`
- `docs/launchify/infrastructure-report.csv`
- `docs/launchify/deployment-report.csv`
- `docs/launchify/verification.md`
- `docs/launchify/manual-validation.md`
- `docs/launchify/production-grade.md`
- `docs/launchify/production-grade.csv`
- `docs/launchify/production-branch.md`
- `docs/launchify/production-branch.csv`
- `docs/launchify/compliance-report.csv`
- `docs/launchify/compliance-summary.md`

---

## Evidence Requirements

For each finding, always capture:
- unique ID, category, severity, confidence
- file and line/range
- affected component, feature, infrastructure resource
- vulnerability or issue description
- evidence, attack prerequisites, exploit path
- impact, remediation, status, verification
- whether runtime validation is required

Never report a vulnerability because a suspicious token exists. Trace actual behavior.

---

## Safety

Read `.launchify/safety.md` before performing any action. Key rules:
- Never claim runtime state without proof
- Read-only by default for infrastructure
- Never expose secrets in output
- Preserve unrelated user changes
- Never automatically rotate secrets
- Never force push, delete branches, or rewrite history unless explicitly requested

---

## Commands

### `/launchify-security`
Full security audit and remediation across 24 categories.

### `/launchify-security-audit`
Full security audit only — no modifications.

### `/launchify-security-{category}`
Audit and remediate a specific security category (24 categories).

### `/launchify-security-{category}-audit`
Audit only for a specific category — no modifications.

### `/launchify-cleanup`
Dead code, duplicates, unused components, AI debris, dependency cleanup.

### `/launchify-cleanup-audit`
Cleanup analysis only — no modifications.

### `/launchify-feature-audit`
Trace every feature lifecycle — complete, underbuilt, overbuilt, broken, abandoned.

### `/launchify-feature-audit-fix`
Audit then safely fix confirmed feature issues.

### `/launchify-verify`
Build, lint, typecheck, tests, dependency integrity, route availability, API contracts.

### `/launchify-report`
Generate or refresh reports from latest findings.

### `/launchify-production-grade`
Score project across 12 dimensions. Letter grade A+ to F.

### `/launchify-production-branch`
Analyze branch diff against main. Merge readiness verdict.

### `/launchify-compliance`
Audit all policies and compliance documents.

### `/launchify-compliance-audit`
Audit only — no modifications.

### `/launchify-landify`
Run everything: security + cleanup + features + compliance + verify + grade.

### `/launchify-landify-audit`
Run everything in audit-only mode — no code modifications.
