# Verification Rules

**Launchify Verification Protocol — Canonical Reference**

---

## Purpose

After any Launchify pass (security, cleanup, feature audit, or remediation), verification ensures that the repository is in a valid, working, production-ready state and that no regressions were introduced.

---

## Verification Flow

### Phase 1: Build Verification

Check that the project builds successfully:
- Run the project's build command
- Verify no build errors
- Verify no new warnings that indicate problems
- Verify build output is consistent with expectations

### Phase 2: Static Analysis

Run all configured static analysis:
- Lint
- Type checking
- Code formatting (verify consistency, do not reformat during verification)
- Security linting
- Dependency auditing

### Phase 3: Test Verification

Run all relevant tests:
- Unit tests
- Integration tests
- End-to-end tests (if available and safe to run)
- Security regression tests
- Feature tests for affected features
- Verify test count has not decreased meaningfully
- Verify no tests were made weaker to pass

### Phase 4: Dependency Integrity

Check dependency health:
- Verify no broken imports
- Verify no missing dependencies
- Verify lockfile consistency
- Verify no dependency version conflicts
- Verify no circular dependencies introduced

### Phase 5: Configuration Integrity

Verify configuration consistency:
- Verify route availability
- Verify API contracts
- Verify public exports
- Verify configuration references
- Verify environment-variable consistency
- Verify migration consistency

### Phase 6: Infrastructure and Deployment

Verify deployment readiness:
- Validate deployment manifests
- Validate container configuration
- Validate Kubernetes manifests (if present)
- Validate Terraform or infrastructure-as-code
- Verify observability configuration
- Verify rollback readiness

### Phase 7: Regression Detection

Detect regressions:
- Broken imports
- Missing runtime registrations
- Removed APIs still referenced
- Accidental permission changes
- Tests made weaker to pass
- Security checks that now fail open
- Features that remain incomplete after remediation
- Deployment configuration that no longer matches application behavior
- Infrastructure resources referenced by code but absent from deployment
- Infrastructure resources deployed but no longer used

### Phase 8: Re-audit Modified Areas

Re-run appropriate Launchify checks against modified areas:
- Security checks on modified security-sensitive code
- Cleanup checks on modified areas
- Feature checks on modified features

---

## Verification Commands

### Build
```
# Detect and run the project's build command
# Common patterns: npm run build, yarn build, pnpm build, make build, cargo build, go build
```

### Lint
```
# Detect and run the project's lint command
# Common patterns: npm run lint, yarn lint, eslint, ruff, clippy
```

### Type Check
```
# Detect and run the project's type check command
# Common patterns: npm run typecheck, tsc --noEmit, mypy, pyright
```

### Tests
```
# Detect and run the project's test command
# Common patterns: npm test, yarn test, jest, vitest, pytest, go test, cargo test
```

---

## Regression Detection Rules

A regression is detected when:

1. **Build breaks** — a previously passing build now fails
2. **Tests fail** — a previously passing test now fails
3. **Type errors** — new type errors appear
4. **Lint errors** — new lint errors appear
5. **Missing exports** — public API surface has shrunk
6. **Missing routes** — previously available routes are now unavailable
7. **Missing dependencies** — imports reference modules that no longer exist
8. **Permission changes** — security permissions have weakened
9. **Test weakening** — tests were modified to pass rather than catching real issues
10. **Security regression** — security checks that previously caught issues now pass

---

## What Verification Must Not Do

- Modify behavior unless necessary to fix a regression introduced by Launchify changes
- Weaken tests to pass verification
- Suppress errors to pass verification
- Disable security checks to pass verification
- Reformat code during verification (that is a cleanup task)
