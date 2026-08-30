# Launchify

Production-readiness skill suite for AI coding agents. Audits, analyzes, and remediates security, infrastructure, architecture, features, and code quality across **Claude Code**, **OpenCode**, and **Codex**.

58 commands. 24 security categories. One canonical specification.

---

## Install

**Claude Code**

```bash
cp -r .claude/skills/launchify /path/to/your/project/.claude/skills/launchify
```

**OpenCode**

```bash
cp -r .opencode/skills/launchify /path/to/your/project/.opencode/skills/launchify
```

**Codex**

```bash
cp AGENTS.md /path/to/your/project/AGENTS.md
```

**Required:** The `.launchify/` directory must be in your project root. All platforms reference it.

```bash
cp -r .launchify /path/to/your/project/.launchify
```

---

## Commands

### Security — Full Audit

| Command | What It Does |
|---|---|
| `/launchify-security` | Audit all 24 categories, fix what's safe, add regression tests, verify fixes |
| `/launchify-security-audit` | Same audit, no code changes — report only |

### Security — Per Category

Every category has two commands: one that audits and fixes, one that audits only.

**Secrets & Configuration**
- `/launchify-security-secrets` — hardcoded secrets, .env files, Git history leaks, secrets in bundles/build artifacts/CI, default credentials, config drift
- `/launchify-security-secrets-audit` — report only

**Authentication**
- `/launchify-security-authentication` — password security, session fixation, JWT flaws, OAuth/SSO misconfig, missing MFA, account enumeration, broken reset flows
- `/launchify-security-authentication-audit` — report only

**Authorization**
- `/launchify-security-authorization` — IDOR, BOLA, cross-tenant access, mass assignment, privilege escalation, unprotected admin routes, missing ownership checks
- `/launchify-security-authorization-audit` — report only

**Database**
- `/launchify-security-database` — SQL/NoSQL injection, missing parameterization, unbounded queries, missing encryption, unsafe migrations, tenant isolation
- `/launchify-security-database-audit` — report only

**API**
- `/launchify-security-api` — unsecured endpoints, missing validation, excessive data exposure, missing rate limits, GraphQL issues, legacy endpoints
- `/launchify-security-api-audit` — report only

**Web**
- `/launchify-security-web` — XSS, CSRF, SSRF, XXE, command injection, path traversal, open redirects, missing security headers, CORS, cookie security
- `/launchify-security-web-audit` — report only

**Frontend**
- `/launchify-security-frontend` — client-side security reliance, exposed source maps, unsafe localStorage, third-party script risks, DOM XSS, prototype pollution
- `/launchify-security-frontend-audit` — report only

**Cloud**
- `/launchify-security-cloud` — overprivileged IAM, wildcard policies, public storage, missing encryption, metadata endpoint exposure, long-lived credentials
- `/launchify-security-cloud-audit` — report only

**Infrastructure**
- `/launchify-security-infrastructure` — network segmentation, container security, Kubernetes RBAC, WAF, vulnerability scanning, server patching, image provenance
- `/launchify-security-infrastructure-audit` — report only

**Deployment**
- `/launchify-security-deployment` — insecure defaults, missing rollback, health checks, environment parity, artifact integrity, direct production access
- `/launchify-security-deployment-audit` — report only

**Dependencies**
- `/launchify-security-dependencies` — vulnerable packages, unpinned deps, typosquatting, missing lockfiles, SBOM, dependency scanning
- `/launchify-security-dependencies-audit` — report only

**CI/CD**
- `/launchify-security-cicd` — exposed CI secrets, untrusted actions, unpinned builds, command injection, missing branch protection, fork PR leaks
- `/launchify-security-cicd-audit` — report only

**Logging**
- `/launchify-security-logging` — sensitive data in logs, missing audit logs, missing log retention, missing time sync
- `/launchify-security-logging-audit` — report only

**Monitoring**
- `/launchify-security-monitoring` — missing security monitoring, anomaly detection, alerting, payment-abuse and AI abuse monitoring
- `/launchify-security-monitoring-audit` — report only

**AI & LLM**
- `/launchify-security-ai` — prompt injection, system prompt leakage, jailbreaks, unsafe output, excessive permissions, unbounded token usage, missing approval gates
- `/launchify-security-ai-audit` — report only

**RAG & Vector**
- `/launchify-security-rag` — exposed vector DBs, cross-tenant retrieval, vector poisoning, document prompt injection, missing tenant-aware indexing
- `/launchify-security-rag-audit` — report only

**AI Agents**
- `/launchify-security-agents` — excessive tool permissions, destructive actions without approval, tool-output injection, memory poisoning, missing audit trails
- `/launchify-security-agents-audit` — report only

**Payments**
- `/launchify-security-payments` — price manipulation, unsigned webhooks, webhook replay, duplicate processing, race conditions, client-controlled entitlements
- `/launchify-security-payments-audit` — report only

**Privacy**
- `/launchify-security-privacy` — PII overcollection, missing encryption, missing retention/deletion, privacy-policy mismatch, missing consent management
- `/launchify-security-privacy-audit` — report only

**Reliability**
- `/launchify-security-reliability` — missing backups, untested restoration, infinite retries, resource exhaustion, missing circuit breakers, unbounded queries
- `/launchify-security-reliability-audit` — report only

**Code Quality**
- `/launchify-security-code-quality` — missing security review, missing threat modeling, missing SAST/DAST, debug code, missing staging parity
- `/launchify-security-code-quality-audit` — report only

**Business Logic**
- `/launchify-security-business-logic` — workflow bypasses, state machine manipulation, race conditions, missing server-side validation, entitlement bypass
- `/launchify-security-business-logic-audit` — report only

**Incident Response**
- `/launchify-security-incident-response` — missing IR plan, missing escalation, missing runbooks, missing forensic preservation, missing post-incident review
- `/launchify-security-incident-response-audit` — report only

**Feature Readiness**
- `/launchify-security-feature-readiness` — missing error handling, missing auth on feature endpoints, missing tenant isolation, missing monitoring
- `/launchify-security-feature-readiness-audit` — report only

### Cleanup

| Command | What It Does |
|---|---|
| `/launchify-cleanup` | Dead code, duplicate logic, unused components, AI debris, dependency cleanup, config cleanup, architecture consistency, test cleanup |
| `/launchify-cleanup-audit` | Same analysis, no code changes |

### Features

| Command | What It Does |
|---|---|
| `/launchify-feature-audit` | Trace every feature lifecycle — classify as complete/underbuilt/overbuilt/broken/abandoned, identify missing requirements |
| `/launchify-feature-audit-fix` | Audit then safely fix confirmed feature issues |

### Verification & Reporting

| Command | What It Does |
|---|---|
| `/launchify-verify` | Build, lint, typecheck, tests, dependency integrity, route availability, API contracts, regression detection |
| `/launchify-report` | Generate or refresh reports from latest findings |

### Production Readiness

| Command | What It Does |
|---|---|
| `/launchify-production-grade` | Score project across 12 dimensions (Security, Reliability, Code Quality, Testing, Infrastructure, Deployment, Features, Monitoring, Dependencies, Documentation, Privacy, Operational Readiness). Produce letter grade A+ through F. |
| `/launchify-production-branch` | Analyze branch diff against main — classify every change as MERGE_READY/NEEDS_FIXES/HOLD/DEV_ONLY/REVERT, produce merge verdict |

---

## How It Works

**1. Understands the repo** — maps structure, frameworks, auth, API, infra, CI/CD, AI integrations, payments, tests before touching anything.

**2. Traces real behavior** — never reports findings from suspicious strings alone. Traces code paths, infrastructure paths, deployment paths, authorization boundaries.

**3. Fixes safely** — smallest correct remediation, updates tests, runs verification, inspects the diff, re-runs the check.

**4. Verifies** — builds, lint, typecheck, tests, dependency integrity, no regressions, no weakened security checks.

---

## Reports

All output goes to `docs/launchify/`. Reports are only generated for commands that ran.

| File | Source Command |
|---|---|
| `security-report.csv` | `/launchify-security*` |
| `security-summary.md` | `/launchify-security*` |
| `security-fixes.md` | `/launchify-security` |
| `cleanup-report.csv` | `/launchify-cleanup*` |
| `cleanup-summary.md` | `/launchify-cleanup*` |
| `feature-report.csv` | `/launchify-feature-audit*` |
| `feature-summary.md` | `/launchify-feature-audit*` |
| `infrastructure-report.csv` | `/launchify-security-infrastructure` |
| `deployment-report.csv` | `/launchify-security-deployment` |
| `production-grade.md` | `/launchify-production-grade` |
| `production-grade.csv` | `/launchify-production-grade` |
| `production-branch.md` | `/launchify-production-branch` |
| `production-branch.csv` | `/launchify-production-branch` |
| `verification.md` | `/launchify-verify` |
| `manual-validation.md` | Any command with findings needing runtime validation |

---

## Safety

- Findings are evidence-backed, never based on suspicious tokens
- Infrastructure checks are read-only by default
- Secrets are never exposed in output
- Unrelated user changes are preserved
- Secrets are never auto-rotated — reported for operator action
- Git history is never force-pushed or rewritten
- Runtime state claims require proof — "appears to permit" not "is"

---

## Platform Consistency

All three adapters (Claude Code, OpenCode, Codex) define the same 58 commands and reference the same `.launchify/` canonical specifications. Platform adapters are lightweight wrappers that translate command triggers into the canonical workflow.

---

## License

MIT
