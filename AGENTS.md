# Launchify — Codex Agent Instructions

**Agent:** launchify
**Trigger:** User types any command starting with `/launchify-`

---

## Overview

Launchify is a production-readiness skill suite that audits, analyzes, and remediates security, infrastructure, architecture, features, and code quality in software projects.

You implement the Launchify canonical specification located at `.launchify/spec.md`.

---

## Before Any Action

**Spec location:** Check for `.launchify/` in the project directory first. If not found, use `~/.launchify/` (global install).

Always read these files in order (using whichever path exists):

1. `{spec_dir}/spec.md` — canonical specification and command definitions
2. `{spec_dir}/safety.md` — safety and production safety rules
3. `{spec_dir}/remediation.md` — remediation rules (for modifying commands)
4. `{spec_dir}/cleanup.md` — cleanup rules (for cleanup commands)
5. `{spec_dir}/verification.md` — verification rules (for verify command)
6. `{spec_dir}/feature-audit.md` — feature audit rules (for feature commands)
7. `{spec_dir}/production-grade.md` — production grading rules (for grade command)
8. `{spec_dir}/production-branch.md` — branch readiness rules (for branch command)

For security commands, also read the relevant category file from `{spec_dir}/categories/`.
For infrastructure commands, also read `{spec_dir}/checks/infrastructure.md`.

---

## Commands

### `/launchify-security`

**Full security audit and remediation.**

1. Establish a repository model by inspecting the project structure, frameworks, languages, databases, authentication, authorization, API definitions, frontend, infrastructure, CI/CD, and deployment
2. For each of the 24 security categories:
   a. Read the category definition from `.launchify/categories/{category}.md`
   b. Perform the checks defined in that category
   c. Trace actual code paths, infrastructure paths, and deployment paths
   d. Produce evidence-backed findings
3. Validate each finding and remove false positives
4. Rank severity (CRITICAL, HIGH, MEDIUM, LOW, INFO)
5. Determine exploitability
6. Fix issues that can safely be fixed following remediation rules
7. Add or update security regression tests
8. Run relevant tests
9. Re-audit modified areas
10. Verify that vulnerabilities are actually resolved
11. Generate final reports in `docs/launchify/` using the schemas from `.launchify/schemas/`

### `/launchify-security-audit`

**Full security audit only — no modifications.**

Perform the exact same assessment as `/launchify-security`, but DO NOT modify production code, infrastructure, deployment configuration, or application behavior.

### `/launchify-security-secrets`

**Audit and remediate secrets & configuration security.** Read `.launchify/categories/secrets.md`. Check: exposed credentials, hardcoded secrets, Git history leaks, public .env files, secrets in bundles/source maps/build artifacts/container layers/infrastructure outputs/CI-CD secrets, default credentials, verbose production errors, configuration drift. Fix issues that can safely be fixed.

### `/launchify-security-secrets-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-authentication`

**Audit and remediate authentication & identity security.** Read `.launchify/categories/authentication.md`. Check: weak passwords, broken reset flows, session fixation, JWT issues, OAuth/SSO misconfiguration, missing MFA, privilege escalation, account enumeration, session management. Fix issues that can safely be fixed.

### `/launchify-security-authentication-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-authorization`

**Audit and remediate authorization & access control.** Read `.launchify/categories/authorization.md`. Check: IDOR, BOLA, cross-user/tenant access, missing ownership checks, unprotected admin routes, mass assignment, excessive permissions, role escalation, missing resource/field-level authorization. Fix issues that can safely be fixed.

### `/launchify-security-authorization-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-database`

**Audit and remediate database & data-access security.** Read `.launchify/categories/database.md`. Check: SQL/NoSQL injection, unsafe queries, missing parameterization, open permissions, public exposure, missing encryption, sensitive data exposure, unbounded queries, unsafe migrations, missing tenant isolation. Fix issues that can safely be fixed.

### `/launchify-security-database-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-api`

**Audit and remediate API security.** Read `.launchify/categories/api.md`. Check: unsecured endpoints, missing auth, broken object-level authorization, missing validation, mass assignment, excessive data exposure, missing rate limits, GraphQL vulnerabilities, legacy endpoints, missing idempotency. Fix issues that can safely be fixed.

### `/launchify-security-api-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-web`

**Audit and remediate web application security.** Read `.launchify/categories/web.md`. Check: XSS, CSRF, SSRF, XXE, command injection, path traversal, open redirects, insecure file uploads, missing security headers, CORS misconfiguration, cookie security, clickjacking, prototype pollution. Fix issues that can safely be fixed.

### `/launchify-security-web-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-frontend`

**Audit and remediate frontend security.** Read `.launchify/categories/frontend.md`. Check: client-side security reliance, frontend secrets, exposed source maps, unsafe localStorage, third-party script risks, DOM-based XSS, prototype pollution, insecure postMessage, exposed feature flags, debug tooling in production. Fix issues that can safely be fixed.

### `/launchify-security-frontend-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-cloud`

**Audit and remediate cloud security.** Read `.launchify/categories/cloud.md`. Check: overprivileged IAM, wildcard policies, public storage, missing encryption, network misconfiguration, metadata endpoint exposure, missing audit logging, excessive cross-account access, long-lived credentials. Fix issues that can safely be fixed.

### `/launchify-security-cloud-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-infrastructure`

**Audit and remediate infrastructure security.** Read `.launchify/categories/infrastructure.md` and `.launchify/checks/infrastructure.md`. Check: network segmentation, container security, Kubernetes RBAC, WAF protections, vulnerability scanning, server patching, infrastructure secrets exposure, deployment safety, image provenance. Fix issues that can safely be fixed.

### `/launchify-security-infrastructure-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-deployment`

**Audit and remediate deployment security.** Read `.launchify/categories/deployment.md`. Check: insecure defaults, missing rollback, missing health checks, configuration drift, environment parity, artifact integrity, mutable images, excessive deployment credentials, direct production access. Fix issues that can safely be fixed.

### `/launchify-security-deployment-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-dependencies`

**Audit and remediate dependency & supply-chain security.** Read `.launchify/categories/dependencies.md`. Check: vulnerable packages, malicious packages, unpinned dependencies, missing lockfiles, typosquatting, install-script risk, missing SBOM, dependency scanning. Fix issues that can safely be fixed.

### `/launchify-security-dependencies-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-cicd`

**Audit and remediate CI/CD security.** Read `.launchify/categories/cicd.md`. Check: exposed CI secrets, untrusted actions, unpinned build actions, excessive build permissions, command injection in CI variables, missing branch protection, missing artifact signing, fork PR secret exposure. Fix issues that can safely be fixed.

### `/launchify-security-cicd-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-logging`

**Audit and remediate logging security.** Read `.launchify/categories/logging.md`. Check: sensitive data in logs, API keys in logs, PII in logs, missing audit logs, exposed logs, missing log retention, missing log integrity, missing time synchronization. Fix issues that can safely be fixed.

### `/launchify-security-logging-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-monitoring`

**Audit and remediate monitoring gaps.** Read `.launchify/categories/monitoring.md`. Check: missing security monitoring, missing anomaly detection, missing alerting, missing authentication monitoring, missing payment-abuse monitoring, missing AI abuse monitoring, missing data-exfiltration monitoring. Fix issues that can safely be fixed.

### `/launchify-security-monitoring-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-ai`

**Audit and remediate AI & LLM security.** Read `.launchify/categories/ai.md`. Check: prompt injection, system prompt leakage, jailbreaks, unsafe AI output, missing output validation, excessive AI permissions, sensitive data in prompts, model endpoint exposure, model abuse, unbounded token usage, missing human approval gates. Fix issues that can safely be fixed.

### `/launchify-security-ai-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-rag`

**Audit and remediate RAG & vector security.** Read `.launchify/categories/rag.md`. Check: exposed vector databases, missing retrieval authorization, cross-tenant retrieval, vector poisoning, document-based prompt injection, deleted documents remaining retrievable, missing tenant-aware indexing, unsafe ingestion. Fix issues that can safely be fixed.

### `/launchify-security-rag-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-agents`

**Audit and remediate AI agent security.** Read `.launchify/categories/agents.md`. Check: excessive tool permissions, unrestricted filesystem/database access, destructive actions without approval, tool-output injection, agent memory poisoning, missing action auditing, agents able to deploy/modify infrastructure, missing rollback capability. Fix issues that can safely be fixed.

### `/launchify-security-agents-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-payments`

**Audit and remediate payment & business-logic security.** Read `.launchify/categories/payments.md`. Check: price manipulation, coupon abuse, refund abuse, subscription bypass, unsigned webhooks, webhook replay, duplicate processing, race conditions, client-controlled entitlement state, missing payment audit logs. Fix issues that can safely be fixed.

### `/launchify-security-payments-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-privacy`

**Audit and remediate data protection & privacy.** Read `.launchify/categories/privacy.md`. Check: PII overcollection, missing encryption, missing retention policies, missing deletion workflows, privacy-policy mismatch, sensitive data in logs/client storage/AI providers, missing consent management, missing data classification. Fix issues that can safely be fixed.

### `/launchify-security-privacy-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-reliability`

**Audit and remediate reliability & recovery.** Read `.launchify/categories/reliability.md`. Check: missing backups, untested restoration, missing rate limiting, infinite retries, resource exhaustion, missing circuit breakers, missing health checks, unbounded queries, missing idempotency, missing graceful degradation. Fix issues that can safely be fixed.

### `/launchify-security-reliability-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-code-quality`

**Audit and remediate code quality & security process.** Read `.launchify/categories/code-quality.md`. Check: unreviewed code, missing security review, missing threat modeling, missing SAST/DAST, dead vulnerable code, debug code, missing security regression tests, missing vulnerability remediation process, missing staging security parity. Fix issues that can safely be fixed.

### `/launchify-security-code-quality-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-business-logic`

**Audit and remediate business logic security.** Read `.launchify/categories/business-logic.md`. Check: workflow bypasses, step skipping, state machine manipulation, race conditions in business flows, missing server-side validation, missing abuse prevention, missing entitlement enforcement, entitlement bypass through API manipulation. Fix issues that can safely be fixed.

### `/launchify-security-business-logic-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-incident-response`

**Audit and remediate incident response gaps.** Read `.launchify/categories/incident-response.md`. Check: no incident response plan, missing breach notification, missing escalation paths, missing incident ownership, missing runbooks, missing forensic preservation, missing post-incident review, missing tabletop exercises. Fix issues that can safely be fixed.

### `/launchify-security-incident-response-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-security-feature-readiness`

**Audit and remediate feature readiness.** Read `.launchify/categories/feature-readiness.md`. Check: missing error handling, missing authorization on feature endpoints, missing tenant isolation, missing retry behavior, missing monitoring, missing documentation, missing accessibility, missing tests, missing deployment configuration. Fix issues that can safely be fixed.

### `/launchify-security-feature-readiness-audit`

**Audit only — no modifications.** Same checks. Do not modify code.

### `/launchify-cleanup`

**Repository cleanup and simplification.**

Read `.launchify/cleanup.md`. Understand the project before deleting anything. Identify dead code, duplicate logic, unused components, unnecessary complexity, AI-generated debris, dependency issues, configuration issues, architectural inconsistencies, incomplete refactors, test issues, and documentation issues. Classify each finding. Make changes incrementally, running tests after each change. Generate reports.

### `/launchify-cleanup-audit`

**Cleanup analysis only — no modifications.**

### `/launchify-feature-audit`

**Audit all features for completeness, security, and production readiness.**

Read `.launchify/feature-audit.md`. Discover all features. Trace each feature's complete lifecycle. Classify each feature. Generate reports.

### `/launchify-feature-audit-fix`

**Feature audit and remediation.**

Run the feature audit, then safely remediate confirmed feature issues. Only modify features when the intended behavior is clear and the change can be verified.

### `/launchify-verify`

**Verify changes and production readiness.**

Read `.launchify/verification.md`. Run builds, lint, type checking, tests. Check dependency integrity, route availability, API contracts. Detect regressions. Re-run appropriate checks against modified areas.

### `/launchify-report`

**Generate or refresh reports.**

Generate or refresh Launchify reports based on the latest analysis without modifying production code.

### `/launchify-production-grade`

**Grade the project on production readiness.**

Read `.launchify/production-grade.md`. Grade the project across 12 dimensions: Security (20%), Reliability (15%), Code Quality (10%), Testing (10%), Infrastructure (10%), Deployment (10%), Feature Completeness (10%), Monitoring (5%), Dependencies (5%), Documentation (5%), Privacy (5%), Operational Readiness (5%). Score each dimension 0-100 with evidence. Calculate weighted overall score. Apply hard fail conditions (any CRITICAL vulnerability = automatic F). Produce letter grade (A+ through F). Generate reports. Do NOT modify code — this is read-only.

### `/launchify-production-branch`

**Analyze branch merge readiness.**

Read `.launchify/production-branch.md`. Identify the current branch and target branch (default: main). Compute the diff. Categorize every change. For each change, evaluate completeness, security, reliability, testing, data integrity, deployment requirements, and documentation. Classify each change (MERGE_READY, MERGE_WITH_CAUTION, NEEDS_FIXES, NEEDS_REVIEW, HOLD, DEV_ONLY, REVERT). Assign risk level per change. Check dependencies between changes. Produce overall verdict (MERGE_NOW, MERGE_WITH_ORDER, PARTIAL_MERGE, HOLD_MERGE, REVERT_AND_MERGE). Generate reports. Do NOT merge anything — this is read-only.

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
