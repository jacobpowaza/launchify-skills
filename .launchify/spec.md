# Launchify — Canonical Specification

**Version:** 1.1.0
**Last Updated:** 2026-08-30

---

## Purpose

Launchify is a production-readiness skill suite for AI coding agents. It takes any software project — AI-built or traditionally built — and aggressively prepares it for production by auditing, analyzing, and remediating security, infrastructure, architecture, features, and code quality.

Launchify behaves like a combined senior application security engineer, penetration tester, cloud security engineer, DevSecOps engineer, principal software engineer, reliability engineer, and product-minded feature reviewer.

Its job is not to generate recommendations. Its job is to understand the repository, trace actual behavior, produce evidence-backed findings, fix issues when the selected command permits it, and verify that the project still works afterward.

---

## Architecture

```
.launchify/
├── spec.md                    # This file — canonical specification
├── categories/                # Security category definitions
│   ├── secrets.md
│   ├── authentication.md
│   ├── authorization.md
│   ├── database.md
│   ├── api.md
│   ├── web.md
│   ├── frontend.md
│   ├── cloud.md
│   ├── infrastructure.md
│   ├── deployment.md
│   ├── dependencies.md
│   ├── cicd.md
│   ├── logging.md
│   ├── monitoring.md
│   ├── ai.md
│   ├── rag.md
│   ├── agents.md
│   ├── payments.md
│   ├── privacy.md
│   ├── reliability.md
│   ├── code-quality.md
│   ├── business-logic.md
│   ├── incident-response.md
│   └── feature-readiness.md
├── checks/
│   └── infrastructure.md      # Infrastructure and deployment checks
├── feature-audit.md           # Feature audit rules
├── production-grade.md        # Production grading rules and rubric
├── production-branch.md       # Branch readiness rules
├── remediation.md             # Remediation rules
├── cleanup.md                 # Cleanup rules
├── verification.md            # Verification rules
├── safety.md                  # Safety and production safety rules
└── schemas/
    ├── security.csv.md        # Security report CSV schema
    ├── cleanup.csv.md         # Cleanup report CSV schema
    ├── feature.csv.md         # Feature report CSV schema
    ├── infrastructure.csv.md  # Infrastructure report CSV schema
    ├── production-grade.csv.md   # Production grade CSV schema
    └── production-branch.csv.md  # Production branch CSV schema
```

---

## Supported Platforms

| Platform | Adapter Location | Native Format |
|---|---|---|
| Claude Code | `.claude/skills/launchify/SKILL.md` | Skill with SKILL.md |
| OpenCode | `.opencode/skills/launchify/SKILL.md` | Skill with SKILL.md |
| Codex | `AGENTS.md` + `.launchify/` specs | Agent instructions |

All three adapters reference the same `.launchify/` canonical specifications. Platform adapters translate the canonical spec into the native format while preserving identical command semantics, audit behavior, and reporting.

---

## Commands

### Full Security Remediation
**Command:** `/launchify-security`

Perform the complete Launchify security audit across every supported security category. Then validate each finding, remove false positives, rank severity, determine exploitability, fix issues that can safely be fixed, add or update security regression tests, run relevant tests, re-audit modified areas, verify that vulnerabilities are actually resolved, and generate final reports.

Do not simply grep for suspicious strings. Understand how the application, infrastructure, deployment configuration, and external services actually behave.

### Full Security Audit Only
**Command:** `/launchify-security-audit`

Perform the exact same full security assessment, but DO NOT modify production code, infrastructure, deployment configuration, or application behavior. It may generate reports and temporary analysis artifacts.

Return: confirmed vulnerabilities, likely vulnerabilities requiring manual validation, affected files, affected infrastructure resources, affected routes/endpoints, exploit path, impact, severity, confidence, proposed remediation, verification strategy, and runtime or cloud access required for confirmation.

### Security Category: Secrets & Configuration
**Command:** `/launchify-security-secrets`

Audit and remediate secrets and configuration security: exposed credentials, hardcoded secrets, Git history leaks, public .env files, secrets in bundles, source maps, build artifacts, container layers, infrastructure outputs, CI/CD secrets, default credentials, verbose production errors, configuration drift. Read `.launchify/categories/secrets.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-secrets-audit`

Audit only — no modifications. Generate report.

### Security Category: Authentication
**Command:** `/launchify-security-authentication`

Audit and remediate authentication and identity security: weak passwords, broken reset flows, session fixation, JWT issues, OAuth/SSO misconfiguration, missing MFA, privilege escalation, account enumeration, session management. Read `.launchify/categories/authentication.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-authentication-audit`

Audit only — no modifications. Generate report.

### Security Category: Authorization
**Command:** `/launchify-security-authorization`

Audit and remediate authorization and access control: IDOR, BOLA, cross-user/tenant access, missing ownership checks, unprotected admin routes, mass assignment, excessive permissions, role escalation, missing resource/field-level authorization. Read `.launchify/categories/authorization.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-authorization-audit`

Audit only — no modifications. Generate report.

### Security Category: Database
**Command:** `/launchify-security-database`

Audit and remediate database and data-access security: SQL/NoSQL injection, unsafe queries, missing parameterization, open permissions, public exposure, missing encryption, sensitive data exposure, unbounded queries, unsafe migrations, missing tenant isolation. Read `.launchify/categories/database.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-database-audit`

Audit only — no modifications. Generate report.

### Security Category: API
**Command:** `/launchify-security-api`

Audit and remediate API security: unsecured endpoints, missing auth, broken object-level authorization, missing validation, mass assignment, excessive data exposure, missing rate limits, GraphQL vulnerabilities, legacy endpoints, missing idempotency. Read `.launchify/categories/api.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-api-audit`

Audit only — no modifications. Generate report.

### Security Category: Web
**Command:** `/launchify-security-web`

Audit and remediate web application security: XSS, CSRF, SSRF, XXE, command injection, path traversal, open redirects, insecure file uploads, missing security headers, CORS misconfiguration, cookie security, clickjacking, prototype pollution. Read `.launchify/categories/web.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-web-audit`

Audit only — no modifications. Generate report.

### Security Category: Frontend
**Command:** `/launchify-security-frontend`

Audit and remediate frontend security: client-side security reliance, frontend secrets, exposed source maps, unsafe localStorage, third-party script risks, DOM-based XSS, prototype pollution, insecure postMessage, exposed feature flags, debug tooling in production. Read `.launchify/categories/frontend.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-frontend-audit`

Audit only — no modifications. Generate report.

### Security Category: Cloud
**Command:** `/launchify-security-cloud`

Audit and remediate cloud security: overprivileged IAM, wildcard policies, public storage, missing encryption, network misconfiguration, metadata endpoint exposure, missing audit logging, excessive cross-account access, long-lived credentials. Read `.launchify/categories/cloud.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-cloud-audit`

Audit only — no modifications. Generate report.

### Security Category: Infrastructure
**Command:** `/launchify-security-infrastructure`

Audit and remediate infrastructure security: network segmentation, container security, Kubernetes RBAC, WAF protections, vulnerability scanning, server patching, infrastructure secrets exposure, deployment safety, image provenance. Read `.launchify/categories/infrastructure.md` and `.launchify/checks/infrastructure.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-infrastructure-audit`

Audit only — no modifications. Generate report.

### Security Category: Deployment
**Command:** `/launchify-security-deployment`

Audit and remediate deployment security: insecure defaults, missing rollback, missing health checks, configuration drift, environment parity, artifact integrity, mutable images, excessive deployment credentials, direct production access. Read `.launchify/categories/deployment.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-deployment-audit`

Audit only — no modifications. Generate report.

### Security Category: Dependencies
**Command:** `/launchify-security-dependencies`

Audit and remediate dependency and supply-chain security: vulnerable packages, malicious packages, unpinned dependencies, missing lockfiles, typosquatting, install-script risk, missing SBOM, dependency scanning. Read `.launchify/categories/dependencies.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-dependencies-audit`

Audit only — no modifications. Generate report.

### Security Category: CI/CD
**Command:** `/launchify-security-cicd`

Audit and remediate CI/CD security: exposed CI secrets, untrusted actions, unpinned build actions, excessive build permissions, command injection in CI variables, missing branch protection, missing artifact signing, fork PR secret exposure. Read `.launchify/categories/cicd.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-cicd-audit`

Audit only — no modifications. Generate report.

### Security Category: Logging
**Command:** `/launchify-security-logging`

Audit and remediate logging security: sensitive data in logs, API keys in logs, PII in logs, missing audit logs, exposed logs, missing log retention, missing log integrity, missing time synchronization. Read `.launchify/categories/logging.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-logging-audit`

Audit only — no modifications. Generate report.

### Security Category: Monitoring
**Command:** `/launchify-security-monitoring`

Audit and remediate monitoring gaps: missing security monitoring, missing anomaly detection, missing alerting, missing authentication monitoring, missing payment-abuse monitoring, missing AI abuse monitoring, missing data-exfiltration monitoring. Read `.launchify/categories/monitoring.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-monitoring-audit`

Audit only — no modifications. Generate report.

### Security Category: AI & LLM
**Command:** `/launchify-security-ai`

Audit and remediate AI and LLM security: prompt injection, system prompt leakage, jailbreaks, unsafe AI output, missing output validation, excessive AI permissions, sensitive data in prompts, model endpoint exposure, model abuse, unbounded token usage, missing human approval gates. Read `.launchify/categories/ai.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-ai-audit`

Audit only — no modifications. Generate report.

### Security Category: RAG & Vector
**Command:** `/launchify-security-rag`

Audit and remediate RAG and vector security: exposed vector databases, missing retrieval authorization, cross-tenant retrieval, vector poisoning, document-based prompt injection, deleted documents remaining retrievable, missing tenant-aware indexing, unsafe ingestion. Read `.launchify/categories/rag.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-rag-audit`

Audit only — no modifications. Generate report.

### Security Category: AI Agents
**Command:** `/launchify-security-agents`

Audit and remediate AI agent security: excessive tool permissions, unrestricted filesystem/database access, destructive actions without approval, tool-output injection, agent memory poisoning, missing action auditing, agents able to deploy/modify infrastructure, missing rollback capability. Read `.launchify/categories/agents.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-agents-audit`

Audit only — no modifications. Generate report.

### Security Category: Payments
**Command:** `/launchify-security-payments`

Audit and remediate payment and business-logic security: price manipulation, coupon abuse, refund abuse, subscription bypass, unsigned webhooks, webhook replay, duplicate processing, race conditions, client-controlled entitlement state, missing payment audit logs. Read `.launchify/categories/payments.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-payments-audit`

Audit only — no modifications. Generate report.

### Security Category: Privacy
**Command:** `/launchify-security-privacy`

Audit and remediate data protection and privacy: PII overcollection, missing encryption, missing retention policies, missing deletion workflows, privacy-policy mismatch, sensitive data in logs/client storage/AI providers, missing consent management, missing data classification. Read `.launchify/categories/privacy.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-privacy-audit`

Audit only — no modifications. Generate report.

### Security Category: Reliability
**Command:** `/launchify-security-reliability`

Audit and remediate reliability and recovery: missing backups, untested restoration, missing rate limiting, infinite retries, resource exhaustion, missing circuit breakers, missing health checks, unbounded queries, missing idempotency, missing graceful degradation. Read `.launchify/categories/reliability.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-reliability-audit`

Audit only — no modifications. Generate report.

### Security Category: Code Quality
**Command:** `/launchify-security-code-quality`

Audit and remediate code quality and security process: unreviewed code, missing security review, missing threat modeling, missing SAST/DAST, dead vulnerable code, debug code, missing security regression tests, missing vulnerability remediation process, missing staging security parity. Read `.launchify/categories/code-quality.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-code-quality-audit`

Audit only — no modifications. Generate report.

### Security Category: Business Logic
**Command:** `/launchify-security-business-logic`

Audit and remediate business logic security: workflow bypasses, step skipping, state machine manipulation, race conditions in business flows, missing server-side validation, missing abuse prevention, missing entitlement enforcement, entitlement bypass through API manipulation. Read `.launchify/categories/business-logic.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-business-logic-audit`

Audit only — no modifications. Generate report.

### Security Category: Incident Response
**Command:** `/launchify-security-incident-response`

Audit and remediate incident response gaps: no incident response plan, missing breach notification, missing escalation paths, missing incident ownership, missing runbooks, missing forensic preservation, missing post-incident review, missing tabletop exercises. Read `.launchify/categories/incident-response.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-incident-response-audit`

Audit only — no modifications. Generate report.

### Security Category: Feature Readiness
**Command:** `/launchify-security-feature-readiness`

Audit and remediate feature readiness: missing error handling, missing authorization on feature endpoints, missing tenant isolation, missing retry behavior, missing monitoring, missing documentation, missing accessibility, missing tests, missing deployment configuration. Read `.launchify/categories/feature-readiness.md`. Fix issues that can safely be fixed.

**Command:** `/launchify-security-feature-readiness-audit`

Audit only — no modifications. Generate report.

### Cleanup + Simplification
**Command:** `/launchify-cleanup`

Perform a repository-wide cleanup, simplification, deduplication, and maintainability pass. The goal is NOT to blindly minimize lines of code. The goal is to remove code and complexity that no longer has a justified purpose while preserving intended functionality, security, reliability, and architecture. First understand the project before deleting anything.

### Cleanup Audit Only
**Command:** `/launchify-cleanup-audit`

Perform the same complete cleanup analysis as `/launchify-cleanup`, but make no production-code changes. Generate a report with findings classified as: `SAFE_TO_REMOVE`, `SAFE_TO_SIMPLIFY`, `REVIEW_REQUIRED`, `LIKELY_INTENTIONAL`, `DO_NOT_TOUCH`.

### Feature Audit
**Command:** `/launchify-feature-audit`

Audit every meaningful product and technical feature in the repository. Determine whether each feature is complete, underbuilt, overbuilt, partially implemented, broken, insecure, unreliable, inconsistent, poorly integrated, missing required edge cases, missing operational support, or abandoned.

### Feature Remediation
**Command:** `/launchify-feature-audit-fix`

Run the feature audit, then safely remediate confirmed feature issues. Only modify features when the intended behavior is clear, the required change is supported by repository evidence, the change can be implemented without inventing product policy, and the change can be verified.

### Verification
**Command:** `/launchify-verify`

Verify the current repository after a Launchify pass. Check builds, lint, type checking, unit tests, integration tests, end-to-end tests, security regression tests, feature tests, dependency integrity, route availability, API contracts, public exports, configuration references, infrastructure validation, deployment manifests, container configuration, Kubernetes manifests, infrastructure-as-code validation, migration consistency, environment-variable consistency, observability configuration, and rollback readiness.

### Reports
**Command:** `/launchify-report`

Generate or refresh Launchify reports based on the latest analysis without intentionally modifying production code.

### Production Grade
**Command:** `/launchify-production-grade`

Grade the entire project on production readiness across 12 dimensions: Security (20%), Reliability (15%), Code Quality (10%), Testing (10%), Infrastructure (10%), Deployment (10%), Feature Completeness (10%), Monitoring (5%), Dependencies (5%), Documentation (5%), Privacy (5%), and Operational Readiness (5%).

For each dimension, score 0-100 based on evidence from the codebase. Produce a letter grade (A+ through F), a weighted overall score, per-dimension breakdowns, and a prioritized remediation path.

This command does NOT modify code. It is a full read-only audit.

Hard fail conditions override the score: any CRITICAL security vulnerability, missing authentication on sensitive endpoints, missing authorization on multi-tenant data, publicly accessible database, hardcoded secrets, no backups, or no rollback mechanism automatically results in an F regardless of other dimension scores.

See `.launchify/production-grade.md` for the complete grading rubric.

### Production Branch
**Command:** `/launchify-production-branch`

Analyze the current branch (or a specified branch) against main and determine what is safe to merge and what must stay on dev.

For every change on the branch (features, pages, endpoints, migrations, config changes, infrastructure changes, dependencies), evaluate completeness, security, reliability, testing, data integrity, deployment requirements, and documentation.

Classify each change as: MERGE_READY, MERGE_WITH_CAUTION, NEEDS_FIXES, NEEDS_REVIEW, HOLD, DEV_ONLY, or REVERT.

Produce a risk assessment per change, a feature-level readiness verdict, dependency ordering if needed, and an overall merge verdict (MERGE_NOW, MERGE_WITH_ORDER, PARTIAL_MERGE, HOLD_MERGE, or REVERT_AND_MERGE).

This command does NOT merge anything. It is read-only.

See `.launchify/production-branch.md` for the complete branch readiness rules.

### Compliance and Policies
**Command:** `/launchify-compliance`

Audit all legal policies, compliance documents, regulatory requirements, and business disclosures. Check: privacy policy, terms of service, cookie policy, EULA, DPA, DMCA, AUP, security statement, refund policy, SLA, accessibility statement, AI disclosures, and regulatory compliance (GDPR, CCPA, HIPAA, SOC 2, COPPA, PCI DSS).

Verify each policy exists, is linked from the product, contains all required clauses, is current (updated within 12 months), and matches actual data practices in code.

**Command:** `/launchify-compliance-audit`

Audit only — no modifications. Generate report.

### Landify (Everything)
**Command:** `/launchify-landify`

Run every Launchify command in sequence. Full production readiness assessment in one command:

1. `/launchify-security` — full security audit and remediation across all 24 categories
2. `/launchify-cleanup` — dead code, duplicates, AI debris, dependency cleanup
3. `/launchify-feature-audit-fix` — trace every feature, fix confirmed issues
4. `/launchify-compliance` — audit all policies and compliance documents
5. `/launchify-verify` — build, lint, typecheck, tests, dependency integrity
6. `/launchify-production-grade` — score across 12 dimensions, letter grade A+ to F

This is the "do everything" command. Run it when you want a complete production readiness pass.

**Command:** `/launchify-landify-audit`

Same as `/launchify-landify` but in audit-only mode — no code modifications across any step.

---

## Security Categories

| Category | ID |
|---|---|
| Secrets & Configuration Security | `secrets` |
| Authentication & Identity Security | `authentication` |
| Authorization & Access Control | `authorization` |
| Database & Data-Access Security | `database` |
| API Security | `api` |
| Web Application Security | `web` |
| Frontend Security | `frontend` |
| Cloud Security | `cloud` |
| Infrastructure & Deployment Security | `infrastructure` |
| Deployment Security | `deployment` |
| Dependency & Supply-Chain Security | `dependencies` |
| CI/CD Security | `cicd` |
| Logging, Monitoring & Response | `logging` |
| Monitoring | `monitoring` |
| AI & LLM Security | `ai` |
| RAG & Vector Security | `rag` |
| AI Agent Security | `agents` |
| Payments & Business Logic | `payments` |
| Data Protection & Privacy | `privacy` |
| Reliability & Recovery | `reliability` |
| Code Quality & Security Process | `code-quality` |
| Business Logic Security | `business-logic` |
| Incident Response | `incident-response` |
| Feature Readiness | `feature-readiness` |
| Compliance & Policies | `compliance` |

---

## Evidence Requirements

For each finding, capture:

- **ID:** unique finding identifier
- **Category:** security category
- **Severity:** CRITICAL, HIGH, MEDIUM, LOW, INFO
- **Confidence:** CONFIRMED, HIGH, MEDIUM, LOW, NEEDS_RUNTIME_VALIDATION, NEEDS_PRODUCT_CLARIFICATION
- **File:** affected file path
- **Location:** line or range when available
- **Component:** affected component
- **Feature:** affected feature
- **Infrastructure Resource:** affected infrastructure resource
- **Vulnerability or Issue:** description
- **Evidence:** supporting evidence
- **Attack Prerequisites:** what an attacker needs
- **Exploit Path:** how the vulnerability is exploited
- **Impact:** business and technical impact
- **Remediation:** fix description
- **Status:** current status
- **Verification:** how to verify the fix
- **Runtime Validation Required:** whether cloud/runtime access is needed

Never report a vulnerability simply because a suspicious token exists. Trace actual code paths, infrastructure paths, deployment paths, feature flows, and authorization boundaries.

---

## Repository Understanding Phase

Before auditing or modifying anything, Launchify must establish a repository model. Inspect:

- repository layout
- workspace or monorepo structure
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
- WAF and API gateways
- monitoring and logging
- AI providers, model calls, agent tool definitions
- RAG pipeline, vector databases
- payment providers, external integrations
- tests, feature flags, product documentation
- user-facing routes, administrative workflows

Determine which code paths are actually production-relevant. Do not treat demos, fixtures, examples, tests, generated code, infrastructure modules, and production code identically.

---

## Remediation Rules

When running a modifying command:

1. Identify the issue
2. Validate that it is real
3. Understand why the current code or configuration exists
4. Identify dependencies
5. Determine whether the issue is code, infrastructure, deployment, policy, or product ambiguity
6. Plan the smallest correct remediation
7. Implement it
8. Update tests
9. Update infrastructure or deployment validation where relevant
10. Run relevant verification
11. Inspect the diff
12. Re-run the affected check
13. Document unresolved manual work

Do not:

- Blindly rewrite large systems
- Replace architecture without cause
- Replace infrastructure without understanding operational dependencies
- Remove backwards compatibility without determining whether it is required
- Weaken tests to make changes pass
- Suppress errors instead of fixing them
- Disable security checks
- Add broad try/catch blocks simply to silence failures
- Hardcode secrets
- Fabricate configuration
- Remove functionality just because understanding it is difficult
- Delete dynamic or runtime-loaded code without confirming it is unused
- Assume AI-generated code is inherently bad
- Invent product requirements
- Make irreversible product decisions without evidence
- Expose production systems during testing
- Perform destructive security testing
- Rotate credentials automatically unless explicitly authorized
- Change cloud IAM broadly without identifying affected workloads
- Change network topology without validating service dependencies
- Remove infrastructure resources solely because they appear unused

---

## Safety Rules

See `.launchify/safety.md` for full safety and production safety rules.

Key principles:

- Distinguish between code-level findings, configuration findings, infrastructure findings, deployment-state findings, policy findings, and product requirements
- Never generate fake certainty about runtime state
- Prefer read-only inspection for infrastructure
- Require explicit authorization for cloud access
- Do not modify production resources without understanding operational dependencies
- Do not expose secrets in output
- Redact credentials and sensitive values
- Record which findings require operator validation
- Inspect Git history where relevant for secrets, abandoned migrations, incomplete refactors
- Preserve unrelated user changes
- Never overwrite unrelated edits
- Never force push, delete branches, or rewrite history unless explicitly requested
- Never automatically rotate leaked secrets — report them for operator action

---

## Cleanup Philosophy

Optimize for:

1. correctness
2. security
3. architectural clarity
4. maintainability
5. consistency
6. simplicity
7. performance where relevant
8. fewer unnecessary dependencies
9. fewer duplicate sources of truth
10. easier future agent and human development

Do NOT optimize for smallest line count. A larger clear implementation is preferable to a smaller opaque implementation.

---

## Feature Audit Philosophy

Optimize for:

1. user value
2. correctness
3. security
4. completeness
5. reliability
6. maintainability
7. operational readiness
8. accessibility
9. observability
10. appropriate complexity

A feature is not complete merely because its primary happy path works. A feature is not overbuilt merely because it contains advanced infrastructure. A feature is underbuilt when important requirements are absent relative to its demonstrated purpose, risk, user impact, or operational context. A feature is overbuilt when complexity, infrastructure, abstraction, or operational burden is not justified by actual requirements or usage.

When product intent is unclear, report the ambiguity instead of inventing a requirement.

---

## Reporting

Store Launchify output in `docs/launchify/` by default. If the project already has an established security, architecture, product, or report directory, use it instead.

Generate only the reports relevant to the commands that ran.

### Security CSV Columns
ID, Category, Severity, Confidence, File, Location, Component, Feature, Infrastructure Resource, Issue, Evidence, Attack Prerequisites, Exploit Path, Impact, Recommendation, Status, Verification, Runtime Validation Required

### Cleanup CSV Columns
ID, Type, Confidence, File, Location, Finding, Evidence, Current Purpose, Recommended Action, Risk, Files Affected, Status, Verification

### Feature CSV Columns
ID, Feature, Category, Status, Classification, Confidence, Entry Points, Files, Services, Data Models, Evidence, Missing Requirements, Security Concerns, Reliability Concerns, Complexity Concerns, User Impact, Business Impact, Recommended Action, Priority, Verification

### Infrastructure CSV Columns
ID, Category, Severity, Confidence, Resource, Environment, File, Location, Finding, Evidence, Exposure, Impact, Recommendation, Status, Runtime Validation, Verification

### Production Grade CSV Columns
Dimension, Score, Grade, Weight, Weighted Score, Finding Count, Critical Findings, High Findings, Medium Findings, Low Findings, Recommendation

### Production Branch CSV Columns
Change ID, Type, Files, Feature, Classification, Risk, Security, Reliability, Testing, Data Integrity, Deployment, Documentation, Blockers, Recommendation

---

## Runtime Security Testing

If the environment permits safely running the local application, Launchify may perform non-destructive validation against localhost or explicitly authorized test environments.

Do NOT attack arbitrary external systems. Do NOT perform destructive exploitation. Do NOT attempt credential theft, data destruction, persistence, denial-of-service, or unauthorized lateral movement. Prefer proof-of-concept validation that demonstrates the issue with minimal impact.

---

## Final Goal

After Launchify finishes, a developer should be able to answer:

- What security problems exist?
- Which are actually exploitable?
- What infrastructure and deployment risks exist?
- Which cloud permissions are excessive?
- Is the network segmented appropriately?
- Are containers and Kubernetes configured safely?
- Are servers and dependencies patched and monitored?
- What was fixed?
- What still requires human, product, cloud, or infrastructure work?
- What code is unnecessary?
- What architecture is duplicated?
- What dependencies are unnecessary?
- What technical debt was created by previous coding agents?
- Which features are underbuilt?
- Which features are overbuilt?
- Which features are unfinished or abandoned?
- Which features lack security, reliability, accessibility, monitoring, or operational support?
- Did cleanup break anything?
- Did feature remediation preserve intended behavior?
- Is the repository materially closer to production readiness?
- What is the overall production grade?
- Which dimensions are weakest?
- What is the highest-priority remediation path?
- Which changes on the current branch are safe to merge to main?
- Which changes must stay on dev?
- What is the riskiest change on the branch?
- Can the branch be merged now, or must it wait?
