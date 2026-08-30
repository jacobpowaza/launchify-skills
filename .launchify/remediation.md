# Remediation Rules

**Launchify Remediation Protocol — Canonical Reference**

---

## Remediation Flow

When running a modifying command (`/launchify-security`, `/launchify-security-{category}`, `/launchify-cleanup`, `/launchify-feature-audit-fix`):

### Phase 1: Identification

1. Identify the issue through code analysis, configuration review, or infrastructure inspection
2. Validate that the issue is real — not a false positive
3. Understand why the current code or configuration exists
4. Identify dependencies and affected components

### Phase 2: Classification

Determine whether the issue is:
- **Code-level** — fixable by modifying source code
- **Infrastructure** — fixable by modifying infrastructure-as-code
- **Deployment-state** — requires operator intervention at deployment time
- **Policy** — requires organizational decision
- **Product ambiguity** — requires product clarification before action

### Phase 3: Planning

6. Plan the smallest correct remediation
7. Determine whether the fix could break other functionality
8. Identify tests that need updating
9. Identify infrastructure or deployment validation that needs updating

### Phase 4: Implementation

10. Implement the fix
11. Update affected tests
12. Update infrastructure or deployment validation where relevant
13. Run relevant verification

### Phase 5: Verification

14. Inspect the diff
15. Re-run the affected check
16. Verify that the vulnerability is actually resolved
17. Verify that no regressions were introduced
18. Document unresolved manual work

---

## Remediation Principles

### Smallest Correct Fix

Always prefer the smallest change that correctly addresses the issue. Do not:
- Blindly rewrite large systems
- Replace architecture without cause
- Replace infrastructure without understanding operational dependencies

### Preserve Intended Behavior

When fixing security or cleanup issues:
- Understand what the code is supposed to do first
- Fix only the unsafe or wasteful aspect
- Preserve the intended functionality
- Ensure tests still pass

### Do Not Weaken Security to Pass Tests

If a test fails because a security check now catches a real issue, fix the underlying code — do not weaken the test.

### Do Not Suppress Errors

If an operation fails, fix the cause. Do not wrap it in try/catch to silence it.

### Do Not Disable Security Checks

If a security check finds a real issue, fix the issue. Do not disable the check.

### Do Not Fabricate Configuration

If configuration is missing, report that it is missing and needs operator setup. Do not invent values.

### Do Not Invent Product Requirements

If product behavior is ambiguous, report the ambiguity. Do not guess what the product should do.

### Do Not Make Irreversible Decisions

Do not make irreversible infrastructure, IAM, or network changes without explicit operator confirmation.

### Document Unresolved Work

When a fix requires operator intervention:
- Clearly document what needs to happen
- Document why Launchify cannot do it automatically
- Document the access or permissions required
- Document the expected impact

---

## What Must Not Be Modified

During remediation, Launchify must not:
- Rewrite large systems without cause
- Replace architecture without understanding dependencies
- Remove backwards compatibility without determining whether it is required
- Weaken tests to make changes pass
- Suppress errors instead of fixing them
- Disable security checks
- Add broad try/catch blocks to silence failures
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
- Remove infrastructure resources solely because they appear unused without checking deployment and operational references

---

## Testing After Remediation

After implementing fixes:
1. Run all relevant unit tests
2. Run all relevant integration tests
3. Run security regression tests
4. Run feature tests for affected features
5. Verify builds pass
6. Verify type checking passes
7. Verify lint passes
8. Re-run the affected Launchify check
9. Verify no regressions in unrelated areas

---

## Documentation After Remediation

After implementing fixes:
1. Update affected documentation
2. Update setup instructions if environment variables changed
3. Update API documentation if endpoints changed
4. Update security documentation if security posture changed
5. Generate or update reports in `docs/launchify/`
