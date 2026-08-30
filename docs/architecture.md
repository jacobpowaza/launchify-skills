# Architecture

## How Launchify Works

Launchify is a **specification-driven** skill suite. The core logic lives in `.launchify/` — a set of markdown files that define exactly what each command does, what it checks, and how it reports findings.

Platform adapters (Claude Code, OpenCode, Codex) are thin wrappers that translate user commands into the canonical workflow defined in the specification.

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

---

## Why Specification-Driven

| Benefit | Explanation |
|---|---|
| **Consistency** | All three platforms produce identical results |
| **Maintainability** | Change the spec once, all platforms update |
| **Portability** | Works on any platform that can read markdown |
| **Transparency** | Users can read exactly what commands do |
| **Extensibility** | Add new categories by adding new markdown files |

---

## Directory Structure

```
launchify-skills/
├── .launchify/                    ← Canonical specification
│   ├── spec.md                    ← Master spec: all 58 commands
│   ├── safety.md                  ← Safety rules (read first)
│   ├── remediation.md             ← 13-step remediation protocol
│   ├── cleanup.md                 ← Cleanup rules and philosophy
│   ├── verification.md            ← Verification protocol
│   ├── feature-audit.md           ← Feature audit rules
│   ├── production-grade.md        ← 12-dimension grading rubric
│   ├── production-branch.md       ← Branch readiness rules
│   ├── categories/                ← 24 security category definitions
│   │   ├── secrets.md
│   │   ├── authentication.md
│   │   ├── authorization.md
│   │   ├── database.md
│   │   ├── api.md
│   │   ├── web.md
│   │   ├── frontend.md
│   │   ├── cloud.md
│   │   ├── infrastructure.md
│   │   ├── deployment.md
│   │   ├── dependencies.md
│   │   ├── cicd.md
│   │   ├── logging.md
│   │   ├── monitoring.md
│   │   ├── ai.md
│   │   ├── rag.md
│   │   ├── agents.md
│   │   ├── payments.md
│   │   ├── privacy.md
│   │   ├── reliability.md
│   │   ├── code-quality.md
│   │   ├── business-logic.md
│   │   ├── incident-response.md
│   │   └── feature-readiness.md
│   ├── checks/
│   │   └── infrastructure.md      ← Infrastructure-specific checks
│   └── schemas/
│       ├── security.csv.md
│       ├── cleanup.csv.md
│       ├── feature.csv.md
│       ├── infrastructure.csv.md
│       ├── production-grade.csv.md
│       └── production-branch.csv.md
├── .claude-plugin/
│   └── plugin.json                ← Claude Code marketplace manifest
├── .codex-plugin/
│   └── plugin.json                ← Codex marketplace manifest
├── .agents/plugins/
│   └── marketplace.json           ← Codex marketplace listing
├── .claude/skills/launchify/
│   └── SKILL.md                   ← Claude Code adapter
├── .opencode/skills/launchify/
│   └── SKILL.md                   ← OpenCode adapter
├── AGENTS.md                      ← Codex agent adapter
├── docs/                          ← This documentation
│   ├── overview.md
│   ├── installation.md
│   ├── architecture.md
│   ├── commands/
│   │   └── README.md
│   └── categories/
│       └── README.md
└── README.md
```

---

## Execution Flow

### 1. Repository Understanding Phase

Before any audit, Launchify establishes a repository model by inspecting:

- Repository layout and workspace structure
- Languages, frameworks, package managers
- Build tooling, runtime entrypoints
- Database, migration system
- Authentication, authorization
- API definitions, frontend applications
- Background workers, queues, scheduled jobs
- Cloud configuration, infrastructure-as-code
- CI/CD, deployment targets
- Containerization, Kubernetes
- Network topology, IAM definitions
- Secret-management systems
- WAF and API gateways
- Monitoring and logging
- AI providers, model calls, agent tool definitions
- RAG pipeline, vector databases
- Payment providers, external integrations
- Tests, feature flags, product documentation

### 2. Audit Phase

For each category:
1. Read the category definition from `.launchify/categories/{category}.md`
2. Perform checks defined in that category
3. Trace actual code paths, infrastructure paths, and deployment paths
4. Produce evidence-backed findings

### 3. Validation Phase

- Validate each finding
- Remove false positives
- Rank severity (CRITICAL → INFO)
- Determine exploitability

### 4. Remediation Phase (modifying commands only)

1. Identify the issue
2. Validate that it is real
3. Understand why the current code exists
4. Identify dependencies
5. Plan the smallest correct remediation
6. Implement it
7. Update tests
8. Run verification
9. Inspect the diff
10. Re-run the affected check
11. Document unresolved manual work

### 5. Verification Phase

- Build, lint, typecheck
- Tests (unit, integration, e2e)
- Dependency integrity
- Route availability
- API contracts
- Regression detection

### 6. Reporting Phase

Generate reports in `docs/launchify/`:
- CSV for machine parsing
- Markdown for human reading
- Separate reports per command group

---

## Evidence Requirements

Every finding includes:

| Field | Description |
|---|---|
| ID | Unique finding identifier |
| Category | Security category |
| Severity | CRITICAL, HIGH, MEDIUM, LOW, INFO |
| Confidence | CONFIRMED, HIGH, MEDIUM, LOW, NEEDS_RUNTIME_VALIDATION |
| File | Affected file path |
| Location | Line or range |
| Component | Affected component |
| Feature | Affected feature |
| Issue | Description |
| Evidence | Supporting evidence |
| Attack Prerequisites | What an attacker needs |
| Exploit Path | How the vulnerability is exploited |
| Impact | Business and technical impact |
| Recommendation | Fix description |
| Status | Current status |
| Verification | How to verify the fix |

---

## Safety Model

Launchify follows strict safety rules:

1. **Evidence-based findings** — Never report a vulnerability because a suspicious token exists. Trace actual behavior.
2. **Read-only by default** — Infrastructure checks are read-only. Cloud access requires explicit authorization.
3. **Secrets protection** — Never expose secrets in output. Redact credentials and sensitive values.
4. **Preserve user changes** — Never overwrite unrelated edits.
5. **No auto-rotation** — Never automatically rotate leaked secrets. Report them for operator action.
6. **No destructive git ops** — Never force push, delete branches, or rewrite history unless explicitly requested.
7. **Runtime claims require proof** — Never generate fake certainty about runtime state.

---

## Adding New Categories

To add a new security category:

1. Create `.launchify/categories/{category}.md` with checks, findings, and verification
2. Add command definitions to `.launchify/spec.md`
3. Add commands to all three platform adapters
4. Add CSV schema to `.launchify/schemas/` if needed
5. Update this documentation

---

## Adding New Command Groups

To add a new command group (beyond security):

1. Create `.launchify/{group-name}.md` with rules and workflow
2. Add command definitions to `.launchify/spec.md`
3. Add commands to all three platform adapters
4. Add CSV schema to `.launchify/schemas/`
5. Update this documentation
