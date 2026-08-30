# Feature Audit Rules

**Launchify Feature Audit Protocol — Canonical Reference**

---

## Purpose

Audit every meaningful product and technical feature in the repository to determine whether each feature is complete, underbuilt, overbuilt, partially implemented, broken, insecure, unreliable, inconsistent, poorly integrated, or abandoned.

---

## Feature Audit Flow

### Phase 1: Feature Discovery

Identify all features by examining:
- User-facing entry points (routes, pages, components, commands)
- Backend routes, endpoints, API handlers
- Service and domain logic
- Database models and migrations
- Background jobs, queues, scheduled tasks
- External integrations
- Feature flags
- Configuration
- Documentation

### Phase 2: Feature Tracing

For each feature, trace the complete lifecycle:
1. Product intent and documentation
2. User-facing entry points
3. Frontend flows
4. Backend routes
5. Service and domain logic
6. Database models and migrations
7. Background jobs, queues, scheduled tasks
8. External integrations
9. Authentication
10. Authorization
11. Tenant isolation
12. Validation
13. Error handling
14. Loading and empty states
15. Retry and recovery behavior
16. Idempotency
17. Rate limits
18. Audit logging
19. Metrics and monitoring
20. Security controls
21. Privacy implications
22. Payment and entitlement logic
23. Configuration
24. Feature flags
25. Deployment requirements
26. Tests
27. Accessibility
28. Localization where relevant
29. Documentation
30. Support and operational workflows

### Phase 3: Classification

Classify each feature using one or more of:

| Classification | Meaning |
|---|---|
| `COMPLETE` | Feature is fully implemented with all required production aspects |
| `UNDERBUILT` | Feature exists but lacks important production requirements |
| `OVERBUILT` | Implementation is materially more complex than requirements justify |
| `PARTIALLY_IMPLEMENTED` | Feature is incomplete — missing key paths or behaviors |
| `BROKEN` | Feature does not work correctly |
| `INSECURE` | Feature has security vulnerabilities |
| `UNRELIABLE` | Feature lacks error handling, retries, or recovery |
| `UNUSED` | Feature exists but is not connected to the user-facing product |
| `DUPLICATED` | Feature overlaps substantially with another feature |
| `ABANDONED` | Feature was started but never completed or is no longer maintained |
| `MISSING_REQUIREMENTS` | Feature lacks requirements that its purpose implies |
| `REVIEW_REQUIRED` | Classification cannot be determined without product clarification |

### Phase 4: Underbuilt Feature Checks

Identify features that lack important production requirements:
- happy-path-only implementation
- missing validation, authorization, tenant isolation
- missing error states, loading states, empty states
- missing retry behavior, timeout handling, idempotency
- missing pagination, limits, audit logs
- missing monitoring, alerts, backups, recovery
- missing data migration, privacy controls, accessibility
- missing mobile or responsive behavior where relevant
- missing abuse prevention, rate limiting
- missing security regression tests, integration tests
- missing documentation, admin or support workflows
- missing feature-flag cleanup, deployment configuration
- missing rollback behavior, user notifications
- missing billing or entitlement enforcement
- missing lifecycle states, deletion or archival behavior

### Phase 5: Overbuilt Feature Checks

Identify features whose implementation is materially more complex than demonstrated requirements:
- unnecessary abstraction layers
- premature extensibility
- unused configuration, unused providers
- multiple competing implementations
- unnecessary microservices, queues, event systems
- unnecessary caching, real-time infrastructure
- unnecessary plugin systems, generic schemas
- unnecessary workflow engines, AI involvement
- unnecessary third-party integrations
- excessive state management, feature flags
- speculative compatibility layers
- infrastructure disproportionate to actual usage
- complex code for a feature with one simple use case

Do not recommend simplification merely because a feature is sophisticated. Determine whether the complexity has a justified operational, security, scale, or product purpose.

### Phase 6: Feature Completion Checks

Determine whether each feature has:
- a clear user-visible purpose
- a complete entry point
- a complete success path
- complete failure paths
- correct authorization
- correct data ownership
- correct persistence
- correct cleanup
- correct notifications
- correct analytics or audit behavior
- correct billing behavior where applicable
- correct integration behavior
- tests
- documentation
- deployment support
- monitoring
- rollback or recovery behavior

### Phase 7: Distinctions

The feature audit must distinguish between:
- a feature that is intentionally minimal
- a feature that is incomplete
- a feature that is intentionally internal
- a feature that is abandoned
- a feature that is overbuilt but justified
- a feature that is overbuilt without justification

The feature audit must not invent product requirements. When requirements are unclear, mark the finding `REVIEW_REQUIRED` and explain what must be clarified.

---

## Feature Audit Output

For each feature, report:
- feature ID
- feature name
- feature category
- user-facing entry points
- affected files
- affected services
- affected data models
- current status
- classification
- evidence
- missing requirements
- security concerns
- reliability concerns
- complexity concerns
- user impact
- business impact
- recommended action
- priority
- confidence
- verification plan
