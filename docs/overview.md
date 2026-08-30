# Launchify Overview

## What It Is

Launchify is a production-readiness skill suite for AI coding agents. It takes any software project and aggressively prepares it for production by auditing, analyzing, and remediating security, infrastructure, architecture, features, and code quality.

It behaves like a combined senior application security engineer, penetration tester, cloud security engineer, DevSecOps engineer, principal software engineer, reliability engineer, and product-minded feature reviewer.

## What It Does

| Area | What Launchify Handles |
|---|---|
| 🔒 **Security** | 24 categories, 58 commands. Scans, validates, and fixes vulnerabilities with evidence-backed findings. |
| 🧹 **Cleanup** | Dead code, duplicates, unused components, AI debris, dependency bloat, architecture drift. |
| 🧩 **Features** | Traces every feature lifecycle — complete, underbuilt, overbuilt, broken, or abandoned. |
| ✅ **Verification** | Builds, lint, typecheck, tests, dependency integrity, route availability, API contracts. |
| 🎓 **Grading** | 12-dimension production score (A+ to F) with hard-fail conditions. |
| 🌿 **Branch Analysis** | Diff every change on a branch, classify merge readiness, produce a verdict. |

## How It Differs From Other Audit Tools

- **Traces real behavior.** Never reports findings from suspicious tokens alone. Traces code paths, infrastructure paths, deployment paths, and authorization boundaries.
- **Fixes safely.** Smallest correct remediation, updates tests, runs verification, inspects the diff, re-runs the check.
- **Cross-platform.** Identical behavior on Claude Code, OpenCode, and Codex via a shared canonical specification.
- **Evidence-backed.** Every finding includes file, line, exploit path, impact, and verification strategy.

## Architecture

```
launchify-skills/
├── .launchify/              ← Canonical specification (shared by all platforms)
│   ├── spec.md              ← All 58 commands defined here
│   ├── safety.md            ← Safety rules
│   ├── remediation.md       ← Remediation protocol
│   ├── cleanup.md           ← Cleanup rules
│   ├── verification.md      ← Verification protocol
│   ├── feature-audit.md     ← Feature audit rules
│   ├── production-grade.md  ← Grading rubric
│   ├── production-branch.md ← Branch readiness rules
│   ├── categories/          ← 24 security category definitions
│   ├── checks/              ← Infrastructure checks
│   └── schemas/             ← Report CSV schemas
├── .claude-plugin/          ← Claude Code plugin manifest
├── .codex-plugin/           ← Codex plugin manifest
├── .agents/plugins/         ← Codex marketplace manifest
├── .claude/skills/          ← Claude Code adapter
├── .opencode/skills/        ← OpenCode adapter
├── AGENTS.md                ← Codex agent adapter
├── docs/                    ← This documentation
└── README.md
```

## Supported Platforms

| Platform | Install Method |
|---|---|
| Claude Code | `/plugin install launchify@launchify-skills` |
| OpenCode | `opencode2 plugin add launchify-skills` |
| Codex | `codex plugin add launchify` |

All three platforms read the same `.launchify/` canonical specification. Platform adapters are lightweight wrappers that translate command triggers into the canonical workflow.
