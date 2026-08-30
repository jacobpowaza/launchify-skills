# 🚀 Launchify

**Production-readiness skill suite for AI coding agents.**

Audit, analyze, and remediate security, infrastructure, architecture, features, and code quality across **Claude Code**, **OpenCode**, and **Codex**.

> 58 commands. 24 security categories. One canonical specification. Identical behavior everywhere.

---

## ⚡ Quick Start

### Claude Code

```bash
/plugin install launchify@launchify-skills
```

### OpenCode

```bash
opencode2 plugin add launchify-skills
```

### Codex

```bash
codex plugin marketplace add launchify-skills
codex plugin add launchify
```

### Manual

```bash
git clone git@github.com:jacobpowaza/launchify-skills.git
cp -r launchify-skills/.launchify /path/to/your/project/
# Then copy the adapter for your platform:
#   Claude Code → .claude-plugin/ + .claude/
#   OpenCode   → .opencode/
#   Codex      → .codex-plugin/ + .agents/ + AGENTS.md
```

> 📖 Full installation guide: [docs/installation.md](docs/installation.md)

---

## 🛡️ Security Commands

### Full Audit

| Command | Description |
|---|---|
| `/launchify-security` | Audit all 24 categories, fix what's safe, add regression tests, verify fixes |
| `/launchify-security-audit` | Same audit, no code changes — report only |

### Per-Category Audit

Every category has **two commands**: one that audits and fixes, one that audits only.

| Category | Command | What It Checks |
|---|---|---|
| 🔑 **Secrets** | `/launchify-security-secrets` | Hardcoded secrets, `.env` leaks, Git history, CI secrets, default creds |
| 🔐 **Authentication** | `/launchify-security-authentication` | Passwords, JWT, OAuth/SSO, MFA, session fixation, account enumeration |
| 🛡️ **Authorization** | `/launchify-security-authorization` | IDOR, BOLA, cross-tenant access, mass assignment, privilege escalation |
| 🗄️ **Database** | `/launchify-security-database` | SQL/NoSQL injection, missing parameterization, unbounded queries |
| 🌐 **API** | `/launchify-security-api` | Unsecured endpoints, missing validation, rate limits, GraphQL issues |
| 🖥️ **Web** | `/launchify-security-web` | XSS, CSRF, SSRF, XXE, command injection, path traversal, CORS |
| 📱 **Frontend** | `/launchify-security-frontend` | Exposed secrets, source maps, DOM XSS, third-party script risks |
| ☁️ **Cloud** | `/launchify-security-cloud` | Overprivileged IAM, public storage, metadata exposure, long-lived creds |
| 🏗️ **Infrastructure** | `/launchify-security-infrastructure` | Containers, K8s RBAC, WAF, patching, image provenance |
| 🚀 **Deployment** | `/launchify-security-deployment` | Insecure defaults, missing rollback, health checks, mutable images |
| 📦 **Dependencies** | `/launchify-security-dependencies` | Vulnerable packages, typosquatting, missing lockfiles, SBOM |
| ⚙️ **CI/CD** | `/launchify-security-cicd` | Exposed CI secrets, untrusted actions, missing branch protection |
| 📝 **Logging** | `/launchify-security-logging` | Sensitive data in logs, missing audit logs, log retention |
| 📊 **Monitoring** | `/launchify-security-monitoring` | Missing alerts, anomaly detection, abuse monitoring |
| 🤖 **AI & LLM** | `/launchify-security-ai` | Prompt injection, system prompt leakage, jailbreaks, token abuse |
| 🔍 **RAG & Vector** | `/launchify-security-rag` | Exposed vector DBs, cross-tenant retrieval, vector poisoning |
| 🕵️ **AI Agents** | `/launchify-security-agents` | Excessive tool perms, destructive actions, memory poisoning |
| 💳 **Payments** | `/launchify-security-payments` | Price manipulation, unsigned webhooks, race conditions |
| 🔒 **Privacy** | `/launchify-security-privacy` | PII overcollection, missing retention, consent management |
| ⏱️ **Reliability** | `/launchify-security-reliability` | Missing backups, no rate limits, no circuit breakers |
| ✨ **Code Quality** | `/launchify-security-code-quality` | Missing security review, SAST/DAST, debug code |
| 🧩 **Business Logic** | `/launchify-security-business-logic` | Workflow bypasses, state manipulation, missing validation |
| 🚨 **Incident Response** | `/launchify-security-incident-response` | No IR plan, missing runbooks, no escalation paths |
| ✅ **Feature Readiness** | `/launchify-security-feature-readiness` | Missing error handling, missing auth, missing tests |

> Append `-audit` to any category command for report-only mode (e.g., `/launchify-security-secrets-audit`)

---

## 🧹 Cleanup Commands

| Command | Description |
|---|---|
| `/launchify-cleanup` | Dead code, duplicates, unused components, AI debris, dependency cleanup |
| `/launchify-cleanup-audit` | Same analysis, no code changes |

Findings are classified as: `SAFE_TO_REMOVE`, `SAFE_TO_SIMPLIFY`, `REVIEW_REQUIRED`, `LIKELY_INTENTIONAL`, `DO_NOT_TOUCH`.

---

## 🧩 Feature Commands

| Command | Description |
|---|---|
| `/launchify-feature-audit` | Trace every feature lifecycle — complete, underbuilt, overbuilt, broken, abandoned |
| `/launchify-feature-audit-fix` | Audit then safely fix confirmed feature issues |

Features are classified into 12 statuses: Complete, Underbuilt, Overbuilt, Partially Implemented, Broken, Insecure, Unreliable, Inconsistent, Poorly Integrated, Missing Edge Cases, Missing Operational Support, Abandoned.

---

## ✅ Verification & Reporting

| Command | Description |
|---|---|
| `/launchify-verify` | Build, lint, typecheck, tests, dependency integrity, route availability, API contracts |
| `/launchify-report` | Generate or refresh reports from latest findings |

---

## 🎓 Production Grading

### `/launchify-production-grade`

Score the project across **12 dimensions** and produce a letter grade (A+ to F):

| Dimension | Weight |
|---|---|
| 🔒 Security | 20% |
| ⏱️ Reliability | 15% |
| ✨ Code Quality | 10% |
| 🧪 Testing | 10% |
| 🏗️ Infrastructure | 10% |
| 🚀 Deployment | 10% |
| 🧩 Feature Completeness | 10% |
| 📊 Monitoring | 5% |
| 📦 Dependencies | 5% |
| 📖 Documentation | 5% |
| 🔒 Privacy | 5% |
| 🔧 Operational Readiness | 5% |

**Hard fail conditions** (automatic F):
- Any CRITICAL security vulnerability
- Missing auth on sensitive endpoints
- Missing authorization on multi-tenant data
- Publicly accessible database
- Hardcoded secrets
- No backups
- No rollback mechanism

---

## 🌿 Branch Analysis

### `/launchify-production-branch`

Analyze the current branch against main and determine merge readiness.

For every change, evaluates:
- Completeness, security, reliability, testing
- Data integrity, deployment requirements, documentation

Classifies each change:
| Classification | Meaning |
|---|---|
| ✅ `MERGE_READY` | Safe to merge |
| ⚠️ `MERGE_WITH_CAUTION` | Mergeable but needs attention |
| ❌ `NEEDS_FIXES` | Must fix before merge |
| 👀 `NEEDS_REVIEW` | Needs human review |
| 🛑 `HOLD` | Do not merge yet |
| 🔧 `DEV_ONLY` | Keep on dev branch |
| ↩️ `REVERT` | Should be reverted |

**Overall verdict:** `MERGE_NOW`, `MERGE_WITH_ORDER`, `PARTIAL_MERGE`, `HOLD_MERGE`, or `REVERT_AND_MERGE`.

---

## 🏗️ How It Works

```
User types command
       ↓
Platform adapter (SKILL.md / AGENTS.md)
       ↓
Reads canonical spec from .launchify/
       ↓
Executes workflow (audit → fix → verify → report)
       ↓
Reports in docs/launchify/
```

1. **Understands the repo** — maps structure, frameworks, auth, API, infra, CI/CD, AI integrations, payments, tests
2. **Traces real behavior** — never reports from suspicious tokens alone. Traces code paths, infrastructure paths, deployment paths, authorization boundaries
3. **Fixes safely** — smallest correct remediation, updates tests, runs verification, inspects the diff, re-runs the check
4. **Verifies** — builds, lint, typecheck, tests, dependency integrity, no regressions, no weakened security checks

> 📖 Full architecture docs: [docs/architecture.md](docs/architecture.md)

---

## 📂 Reports

All output goes to `docs/launchify/`. Reports are only generated for commands that ran.

| File | Source |
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
| `manual-validation.md` | Commands with findings needing runtime validation |

---

## 🛡️ Safety

- Evidence-backed findings — never based on suspicious tokens
- Infrastructure checks are read-only by default
- Secrets are never exposed in output
- Unrelated user changes are preserved
- Secrets are never auto-rotated — reported for operator action
- Git history is never force-pushed or rewritten
- Runtime state claims require proof — "appears to permit" not "is"

---

## 📚 Documentation

| Document | Description |
|---|---|
| [Overview](docs/overview.md) | What Launchify is and how it differs from other tools |
| [Installation](docs/installation.md) | Platform-specific installation guides |
| [Architecture](docs/architecture.md) | How the specification-driven system works |
| [Commands](docs/commands/README.md) | Complete command reference |
| [Categories](docs/categories/README.md) | Detailed explanation of all 24 security categories |
| [Canonical Spec](.launchify/spec.md) | The full specification (source of truth) |

---

## 🤝 Contributing

To add a new security category:

1. Create `.launchify/categories/{category}.md`
2. Add commands to `.launchify/spec.md`
3. Add commands to all three platform adapters
4. Add CSV schema to `.launchify/schemas/`
5. Update documentation

---

## 📄 License

MIT
