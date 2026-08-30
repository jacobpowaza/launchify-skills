# Production Branch Rules

**Launchify Production Branch Protocol — Canonical Reference**

---

## Purpose

Analyze the current branch (or a specified branch) and determine what is safe to merge to main and what must stay on dev. Produce a merge-readiness verdict for every feature, page, component, route, endpoint, migration, configuration change, and infrastructure change.

---

## Production Branch Flow

### Phase 1: Branch Context

1. Identify the current branch (or the branch being analyzed)
2. Identify the target branch (default: main)
3. Compute the diff between the branch and the target
4. Identify all files changed, added, or deleted
5. Identify all commits on the branch not on main
6. Identify the branch point (where it diverged from main)

### Phase 2: Change Inventory

Categorize every change on the branch:

| Change Type | Description |
|---|---|
| `feature` | New user-facing feature |
| `page` | New or modified page/route |
| `component` | New or modified UI component |
| `endpoint` | New or modified API endpoint |
| `model` | Database model change |
| `migration` | Database migration |
| `config` | Configuration change |
| `infrastructure` | Infrastructure-as-code change |
| `dependency` | Dependency addition, removal, or upgrade |
| `refactor` | Code refactoring |
| `fix` | Bug fix |
| `security` | Security-related change |
| `test` | Test addition or modification |
| `documentation` | Documentation change |
| `cleanup` | Dead code removal, simplification |

### Phase 3: Per-Change Assessment

For each change, evaluate:

#### 3a. Completeness
- Is the change complete? (no placeholders, no TODOs, no half-implemented logic)
- Is the happy path implemented?
- Are error paths implemented?
- Are edge cases handled?
- Are loading, empty, and error states implemented?
- Is the change self-contained? (does not leave orphaned references)

#### 3b. Security
- Does the change introduce new attack surface?
- Are new endpoints authenticated?
- Are new endpoints authorized?
- Is input validated?
- Are new secrets introduced? (and are they managed properly)
- Are new dependencies introduced? (and are they safe)
- Does the change affect existing security controls?
- Are there any CRITICAL or HIGH security findings in the changed code?

#### 3c. Reliability
- Does the change handle errors gracefully?
- Does the change have retry/recovery behavior?
- Does the change have appropriate timeouts?
- Does the change have rate limiting?
- Does the change have idempotency where needed?
- Does the change have logging and monitoring?
- Could the change cause resource exhaustion?
- Could the change cause data corruption?

#### 3d. Testing
- Are there tests for the changed code?
- Do existing tests still pass?
- Are there security regression tests?
- Are there integration tests?
- Are there end-to-end tests for critical paths?

#### 3e. Data Integrity
- Does the change include a migration?
- Is the migration reversible?
- Does the migration have a rollback plan?
- Does the migration preserve existing data?
- Does the migration have a dry-run mode?
- Is the migration idempotent?
- Does the migration coordinate with deployment order?

#### 3f. Deployment
- Does the change require deployment coordination?
- Does the change require environment variable changes?
- Does the change require infrastructure changes?
- Does the change require secrets to be provisioned?
- Does the change require database migrations?
- Does the change require cache invalidation?
- Does the change require feature flags?
- Does the change affect the deployment manifest?

#### 3g. Documentation
- Is the change documented?
- Are API changes documented?
- Are new environment variables documented?
- Are new features documented?
- Are deployment steps documented?

### Phase 4: Readiness Classification

Classify each change as:

| Classification | Meaning |
|---|---|
| `MERGE_READY` | Safe to merge to main right now |
| `MERGE_WITH_CAUTION` | Safe to merge but requires monitoring after merge |
| `NEEDS_FIXES` | Cannot merge until specific issues are resolved |
| `NEEDS_REVIEW` | Requires human review before merge decision |
| `HOLD` | Should not merge — significant risk or incomplete work |
| `DEV_ONLY` | Intentionally experimental or incomplete — keep on dev |
| `REVERT` | Should be reverted — introduces regression or vulnerability |

### Phase 5: Feature-Level Readiness

Group changes by feature and produce a per-feature readiness verdict:

For each feature:
- What files are involved?
- What is the feature's completeness?
- What is the feature's security posture?
- What is the feature's reliability posture?
- Is the feature tested?
- Is the feature documented?
- Does the feature have operational support?
- Can the feature be safely disabled if something goes wrong?
- Is the feature behind a feature flag?

### Phase 6: Risk Assessment

For each change, assign a risk level:

| Risk Level | Meaning |
|---|---|
| `NONE` | No risk — documentation, tests, or trivial changes |
| `LOW` | Minor change with full test coverage and no security impact |
| `MEDIUM` | Moderate change affecting existing behavior or adding new endpoints |
| `HIGH` | Significant change affecting data, security, infrastructure, or deployment |
| `CRITICAL` | Change that could cause data loss, security breach, or outage |

### Phase 7: Dependency Analysis

Check whether the branch changes have dependencies:
- Are there database migrations that must run before the code deploys?
- Are there infrastructure changes that must be applied before the code deploys?
- Are there secrets that must be provisioned before the code deploys?
- Are there configuration changes that must be applied first?
- Do multiple changes on the branch depend on each other?
- Are there merge conflicts with main?

### Phase 8: Verdict

Produce a final verdict:

| Verdict | Meaning |
|---|---|
| `MERGE_NOW` | All changes are merge-ready. Merge to main. |
| `MERGE_WITH_ORDER` | Changes are merge-ready but must be merged in a specific order. |
| `PARTIAL_MERGE` | Some changes are merge-ready. Create a sub-branch with only safe changes. |
| `HOLD_MERGE` | Significant issues exist. Do not merge until resolved. |
| `REVERT_AND_MERGE` | Revert problematic changes, then merge the remainder. |

---

## Output Format

### Summary Report (`docs/launchify/production-branch.md`)

```markdown
# Launchify Production Branch Report

**Date:** {date}
**Branch:** {branch name}
**Target:** main
**Verdict:** {VERDICT}

## Summary
- Total changes: {count}
- MERGE_READY: {count}
- MERGE_WITH_CAUTION: {count}
- NEEDS_FIXES: {count}
- NEEDS_REVIEW: {count}
- HOLD: {count}
- DEV_ONLY: {count}
- REVERT: {count}

## Risk Summary
- CRITICAL risk changes: {count}
- HIGH risk changes: {count}
- MEDIUM risk changes: {count}
- LOW risk changes: {count}

## Merge-Ready Changes
{list of changes safe to merge}

## Changes Needing Fixes
{list of changes that need fixes before merge}

## Changes Needing Review
{list of changes that need human review}

## Held Changes
{list of changes that should not merge}

## Dev-Only Changes
{list of changes that are intentionally on dev}

## Feature Readiness
{per-feature readiness verdicts}

## Dependency Order
{if MERGE_WITH_ORDER, the required merge sequence}

## Risk Details
{per-change risk assessment}

## Unresolved Items
{items requiring human, product, or infrastructure decisions}
```

### CSV Report (`docs/launchify/production-branch.csv`)

| Column | Description |
|---|---|
| Change ID | Unique identifier for the change |
| Type | Change type (feature, page, endpoint, etc.) |
| Files | Affected files |
| Feature | Feature name (if applicable) |
| Classification | MERGE_READY, NEEDS_FIXES, etc. |
| Risk | NONE, LOW, MEDIUM, HIGH, CRITICAL |
| Security | Security assessment |
| Reliability | Reliability assessment |
| Testing | Test coverage assessment |
| Data Integrity | Migration/data assessment |
| Deployment | Deployment requirements |
| Documentation | Documentation status |
| Blockers | Specific issues blocking merge |
| Recommendation | Recommended action |

---

## Important Rules

1. This command does NOT merge anything. It is read-only — it produces a report.
2. It analyzes the branch diff against main, not the entire codebase.
3. Every classification must be backed by evidence from the actual code changes.
4. Do not assume changes are safe — verify by reading the actual code.
5. If a change is ambiguous, classify as NEEDS_REVIEW and explain what must be clarified.
6. The verdict is advisory — the developer makes the final merge decision.
7. When in doubt, classify conservatively (NEEDS_REVIEW or HOLD).
8. This command can be run on any branch, not just the current branch.
9. If the branch has merge conflicts, report them as blockers.
10. If the branch has been rebased or force-pushed, note that in the report.
