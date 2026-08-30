# Security Categories

Launchify covers 24 security categories. Each category has two commands:

- **`/launchify-security-{category}`** — Audit and fix
- **`/launchify-security-{category}-audit`** — Audit only, no changes

---

## Secrets & Configuration

**Command:** `/launchify-security-secrets`

**What it checks:**
- Hardcoded API keys, tokens, passwords in source code
- Secrets in Git history (even after removal)
- `.env` files committed to the repo
- Secrets leaked in bundles, source maps, build artifacts
- Secrets exposed in Docker container layers
- Secrets in infrastructure-as-code outputs (Terraform, CloudFormation)
- CI/CD pipeline secrets exposed in logs or artifacts
- Default credentials on databases, services, admin panels
- Verbose error messages leaking secrets in production
- Configuration drift between environments

**Common findings:**
- `API_KEY = "sk-..."` in source code
- `.env` in `.gitignore` but already tracked
- AWS keys in Terraform state files
- Database passwords in Docker Compose files
- JWT secrets hardcoded in config

**Why it matters:** A single exposed secret can compromise an entire system. Automated scanners crawl GitHub for leaked credentials within minutes of a push.

---

## Authentication

**Command:** `/launchify-security-authentication`

**What it checks:**
- Weak password policies
- Broken password reset flows
- Session fixation vulnerabilities
- JWT algorithm confusion, missing expiration, weak signing
- OAuth/SSO misconfiguration (open redirect, token leakage)
- Missing multi-factor authentication on sensitive endpoints
- Privilege escalation through auth bypass
- Account enumeration via login/register/error responses
- Session management (concurrent sessions, timeout, revocation)

**Common findings:**
- JWT using `alg: none`
- Password reset token not expiring
- Login endpoint leaking whether a user exists
- Missing MFA on admin accounts
- OAuth callback not validating state parameter

**Why it matters:** Authentication is the front door. If it's broken, everything behind it is exposed.

---

## Authorization

**Command:** `/launchify-security-authorization`

**What it checks:**
- Insecure Direct Object References (IDOR)
- Broken Object Level Authorization (BOLA)
- Cross-user or cross-tenant data access
- Missing ownership checks on resources
- Unprotected admin routes
- Mass assignment vulnerabilities
- Excessive role permissions
- Role escalation through parameter manipulation
- Missing resource-level or field-level authorization

**Common findings:**
- `GET /api/users/:id` returns any user's data without ownership check
- Admin routes behind client-side checks only
- User can modify `role` field via API mass assignment
- Multi-tenant app serving data across tenants

**Why it matters:** Authorization bugs are the most common cause of data breaches. They allow attackers to access data they shouldn't see.

---

## Database

**Command:** `/launchify-security-database`

**What it checks:**
- SQL injection (including blind and second-order)
- NoSQL injection
- Unsafe raw queries without parameterization
- Database permissions too broad
- Public database exposure (missing network restrictions)
- Missing encryption at rest
- Sensitive data stored unencrypted
- Unbounded queries (no pagination, no limits)
- Unsafe database migrations
- Missing tenant isolation in shared databases

**Common findings:**
- String concatenation in SQL queries
- MongoDB `$where` with user input
- Database accessible from 0.0.0.0/0
- PII stored in plaintext columns
- Migration dropping columns without backup

**Why it matters:** Database compromise means full data exposure. SQL injection remains in the OWASP Top 10.

---

## API

**Command:** `/launchify-security-api`

**What it checks:**
- Unauthenticated API endpoints
- Missing API authentication middleware
- Broken Object-Level Authorization (BOLA)
- Missing input validation on endpoints
- Mass assignment on API models
- Excessive data exposure in responses
- Missing rate limiting
- GraphQL introspection enabled in production
- Legacy/deprecated endpoints still accessible
- Missing idempotency on mutation endpoints

**Common findings:**
- `POST /api/admin/users` has no auth middleware
- API returns full user objects including `password_hash`
- No rate limiting on login endpoint
- GraphQL `__schema` query accessible in production
- Deprecated `/v1/` endpoints still live

**Why it matters:** APIs are the primary attack surface for modern applications. Unsecured APIs expose data, enable abuse, and bypass UI-level protections.

---

## Web Application

**Command:** `/launchify-security-web`

**What it checks:**
- Cross-Site Scripting (XSS) — stored, reflected, DOM-based
- Cross-Site Request Forgery (CSRF)
- Server-Side Request Forgery (SSRF)
- XML External Entity (XXE) injection
- Command injection via user input
- Path traversal and directory traversal
- Open redirect vulnerabilities
- Insecure file uploads (unrestricted type, no size limit)
- Missing security headers (CSP, HSTS, X-Frame-Options)
- CORS misconfiguration (wildcard origin, credentials allowed)
- Cookie security (missing Secure, HttpOnly, SameSite)
- Clickjacking (missing X-Frame-Options)
- Prototype pollution

**Common findings:**
- User input rendered as raw HTML
- No CSRF token on state-changing forms
- Server fetches user-supplied URLs without validation
- XML parser resolving external entities
- `Access-Control-Allow-Origin: *` with credentials

**Why it matters:** Web vulnerabilities are the most direct path to user compromise. XSS steals sessions, SSRF attacks internal infrastructure, CSRF forces unintended actions.

---

## Frontend

**Command:** `/launchify-security-frontend`

**What it checks:**
- Client-side security reliance (auth checks in JS only)
- Secrets embedded in frontend code
- Exposed source maps in production
- Unsafe localStorage/sessionStorage usage
- Third-party script risks (CDN compromise, supply chain)
- DOM-based XSS
- Prototype pollution via frontend libraries
- Insecure postMessage handling
- Exposed feature flags in client bundle
- Debug tooling left in production builds

**Common findings:**
- Admin permission check only in React component, not API
- `NEXT_PUBLIC_API_KEY` in client bundle
- Source maps enabled in production
- `localStorage` storing JWT tokens
- Third-party analytics script loading arbitrary code

**Why it matters:** Frontend code runs in the user's browser. Anything in it is accessible to attackers. Client-side security is a defense-in-depth layer, not a control.

---

## Cloud

**Command:** `/launchify-security-cloud`

**What it checks:**
- Overprivileged IAM roles and policies
- Wildcard (`*`) permissions in IAM policies
- Public S3 buckets or storage accounts
- Missing encryption on storage and databases
- Network misconfiguration (public subnets, open security groups)
- Metadata endpoint exposure (SSRF → IAM credentials)
- Missing CloudTrail or audit logging
- Excessive cross-account access
- Long-lived credentials instead of temporary tokens
- Missing resource-level permissions

**Common findings:**
- IAM policy with `"Action": "*"` on `"Resource": "*"`
- S3 bucket with public read access
- EC2 instance metadata endpoint accessible without IMDSv2
- CloudTrail not enabled in all regions
- IAM user with permanent access keys

**Why it matters:** Cloud misconfigurations are the leading cause of data breaches in cloud environments. A single public S3 bucket can expose millions of records.

---

## Infrastructure

**Command:** `/launchify-security-infrastructure`

**What it checks:**
- Network segmentation (flat networks, missing VLANs)
- Container security (running as root, privileged containers, writable filesystems)
- Kubernetes RBAC (excessive permissions, missing NetworkPolicies)
- WAF protections (missing or misconfigured)
- Vulnerability scanning (not enabled or not enforced)
- Server patching (outdated OS, missing security updates)
- Infrastructure secrets exposure (Terraform state, Ansible vault)
- Deployment safety (no canary, no blue-green, no rollback)
- Image provenance (unsigned images, no image scanning)

**Common findings:**
- Container running as `root` with `--privileged`
- Kubernetes pod with `hostNetwork: true`
- No WAF on public-facing load balancer
- EC2 instances running outdated AMIs
- Terraform state file stored locally without encryption

**Why it matters:** Infrastructure is the foundation. If the foundation is compromised, everything on it is at risk.

---

## Deployment

**Command:** `/launchify-security-deployment`

**What it checks:**
- Insecure deployment defaults (debug mode, verbose errors)
- Missing rollback mechanisms
- Missing health checks
- Configuration drift between environments
- Environment parity (dev ≠ staging ≠ prod)
- Artifact integrity (unsigned, unverified builds)
- Mutable Docker images (tags that change)
- Excessive deployment credentials
- Direct production access (SSH, console)
- Missing deployment audit trail

**Common findings:**
- `DEBUG=True` in production config
- No health check endpoint
- Manual SSH access to production servers
- Docker image tagged as `latest` without version pinning
- Deployment credentials with admin access

**Why it matters:** Deployment is where code meets reality. Insecure deployments expose production systems to compromise.

---

## Dependencies

**Command:** `/launchify-security-dependencies`

**What it checks:**
- Known vulnerable packages (CVE matching)
- Malicious packages (typosquatting, dependency confusion)
- Unpinned dependencies (no version constraints)
- Missing lockfiles (package-lock.json, yarn.lock, go.sum)
- Typosquatting (similar names to popular packages)
- Install-script risk (postinstall scripts in dependencies)
- Missing Software Bill of Materials (SBOM)
- Dependency scanning not enabled in CI

**Common findings:**
- `lodash` at version `4.17.20` (known CVE)
- `event-stream` incident (malicious dependency)
- `npm install` without lockfile
- No `npm audit` or `cargo audit` in CI
- Dependency tree with 2000+ transitive dependencies

**Why it matters:** Dependencies are the most common vector for supply chain attacks. The Log4Shell vulnerability affected millions of applications through a single transitive dependency.

---

## CI/CD

**Command:** `/launchify-security-cicd`

**What it checks:**
- Exposed CI/CD secrets (in logs, artifacts, environment)
- Untrusted GitHub Actions (third-party actions without review)
- Unpinned build actions (using `@main` instead of `@sha`)
- Excessive build permissions (write-all, admin tokens)
- Command injection via CI/CD variables
- Missing branch protection rules
- Missing artifact signing
- Fork PR secret exposure
- CI/CD pipeline accessible without auth

**Common findings:**
- GitHub Actions using `actions/checkout@main` (mutable tag)
- Build step echoing secrets to logs
- CI token with `repo` scope for read-only tasks
- No branch protection on `main`
- Fork PRs can access repository secrets

**Why it matters:** CI/CD is the crown jewel. Compromising it means compromising every deployment.

---

## Logging

**Command:** `/launchify-security-logging`

**What it checks:**
- Sensitive data in logs (passwords, tokens, PII)
- API keys logged in request/response logs
- PII logged without consent
- Missing audit logs for security events
- Logs accessible without authentication
- Missing log retention policies
- Missing log integrity protection
- Missing time synchronization across services

**Common findings:**
- Password logged in request body
- JWT token logged in authorization header
- No audit log for failed login attempts
- Logs stored in publicly accessible S3 bucket
- No log rotation or retention policy

**Why it matters:** Logs are both a security control and a liability. Poorly managed logs leak secrets; missing logs make incident response impossible.

---

## Monitoring

**Command:** `/launchify-security-monitoring`

**What it checks:**
- Missing security monitoring (no IDS/IPS, no SIEM)
- Missing anomaly detection
- Missing alerting on security events
- Missing authentication monitoring (brute force, credential stuffing)
- Missing payment abuse monitoring
- Missing AI abuse monitoring (token abuse, prompt injection attempts)
- Missing data exfiltration monitoring

**Common findings:**
- No alerts on repeated failed logins
- No monitoring for unusual API usage patterns
- No alerts on large data exports
- No rate limiting on AI endpoints
- No monitoring for privilege escalation attempts

**Why it matters:** You can't stop what you can't see. Monitoring is the difference between detecting a breach in minutes versus months.

---

## AI & LLM

**Command:** `/launchify-security-ai`

**What it checks:**
- Prompt injection vulnerabilities
- System prompt leakage
- Jailbreak resistance
- Unsafe AI output (no filtering, no validation)
- Missing output validation before downstream use
- Excessive AI permissions (file access, database, exec)
- Sensitive data included in prompts
- Model endpoint exposure (unauthenticated API access)
- Model abuse (no usage limits, no abuse detection)
- Unbounded token usage (no cost controls)
- Missing human approval gates for critical actions

**Common findings:**
- User input concatenated directly into system prompts
- System prompt returned in error messages
- AI agent with `exec` permission and no approval gate
- No token usage limits (runaway costs)
- PII sent to external AI provider without redaction

**Why it matters:** AI/LLM security is an emerging attack surface. Prompt injection can bypass all application security controls.

---

## RAG & Vector

**Command:** `/launchify-security-rag`

**What it checks:**
- Exposed vector databases (no authentication)
- Missing retrieval authorization (any user queries all documents)
- Cross-tenant retrieval in multi-tenant RAG
- Vector poisoning (malicious documents influencing retrieval)
- Document-based prompt injection
- Deleted documents still retrievable from vector store
- Missing tenant-aware indexing
- Unsafe document ingestion (no sanitization)

**Common findings:**
- Vector DB accessible without auth
- RAG pipeline serving documents across tenants
- No document-level access control
- User-uploaded documents not sanitized before indexing
- Deleted documents remaining in vector index

**Why it matters:** RAG systems expose internal documents to AI. Without proper access control, anyone can query your entire knowledge base.

---

## AI Agents

**Command:** `/launchify-security-agents`

**What it checks:**
- Excessive tool permissions (filesystem, database, exec)
- Unrestricted filesystem access
- Destructive actions without approval (delete, drop, overwrite)
- Tool-output injection (attacker-controlled data in tool results)
- Agent memory poisoning
- Missing action auditing
- Agents able to deploy or modify infrastructure
- Missing rollback capability

**Common findings:**
- Agent with `bash` tool and no command restrictions
- Agent can modify database without approval
- No audit log of agent actions
- Agent can deploy to production
- No rollback mechanism for agent changes

**Why it matters:** AI agents have superuser access by default. Without guardrails, a compromised agent can destroy your entire system.

---

## Payments

**Command:** `/launchify-security-payments`

**What it checks:**
- Price manipulation (client-controlled pricing)
- Coupon abuse (reuse, stacking, generation)
- Refund abuse (duplicate refunds, amount manipulation)
- Subscription bypass (client-side validation only)
- Unsigned webhooks (no signature verification)
- Webhook replay attacks
- Duplicate processing (no idempotency)
- Race conditions in payment flows
- Client-controlled entitlement state
- Missing payment audit logs

**Common findings:**
- Price sent from client instead of server
- No webhook signature verification
- Coupon code not invalidated after use
- Race condition allowing double refund
- No idempotency key on payment endpoint

**Why it matters:** Payment vulnerabilities directly cause financial loss. They are the most commonly exploited class of business logic bugs.

---

## Privacy

**Command:** `/launchify-security-privacy`

**What it checks:**
- PII overcollection (collecting more than needed)
- Missing encryption for PII at rest and in transit
- Missing data retention policies
- Missing deletion workflows (right to be forgotten)
- Privacy policy mismatch (policy says one thing, code does another)
- Sensitive data in logs, client storage, or AI providers
- Missing consent management
- Missing data classification

**Common findings:**
- Collecting full address when only city is needed
- PII stored unencrypted in database
- No data retention/deletion policy
- Privacy policy claims encryption but data is plaintext
- User data sent to AI provider without consent

**Why it matters:** Privacy violations cause regulatory fines (GDPR, CCPA) and user trust erosion. They are also increasingly litigated.

---

## Reliability

**Command:** `/launchify-security-reliability`

**What it checks:**
- Missing backups
- Untested backup restoration
- Missing rate limiting
- Infinite retries without backoff
- Resource exhaustion (memory, connections, file handles)
- Missing circuit breakers
- Missing health checks
- Unbounded database queries
- Missing idempotency on critical operations
- Missing graceful degradation

**Common findings:**
- No database backup configured
- API retry with no delay (thundering herd)
- No connection pool limits
- No circuit breaker on external service
- No health check endpoint for load balancer

**Why it matters:** Reliability bugs become outages. The cost of downtime is measured in revenue, reputation, and regulatory compliance.

---

## Code Quality

**Command:** `/launchify-security-code-quality`

**What it checks:**
- Unreviewed code (no PR review process)
- Missing security review for sensitive changes
- Missing threat modeling
- Missing SAST/DAST in CI pipeline
- Dead vulnerable code (old code with known CVEs)
- Debug code left in production
- Missing security regression tests
- Missing vulnerability remediation process
- Missing staging/security parity

**Common findings:**
- No security review required for PRs
- `console.log` and `debugger` statements in production
- No SAST tool in CI pipeline
- Known vulnerable function in use (e.g., `eval()`)
- Staging environment differs from production

**Why it matters:** Code quality is a security multiplier. Poor code quality makes vulnerabilities harder to find and fix.

---

## Business Logic

**Command:** `/launchify-security-business-logic`

**What it checks:**
- Workflow bypasses (skipping steps in multi-step flows)
- Step skipping (completing a flow without required中间 steps)
- State machine manipulation (forcing invalid state transitions)
- Race conditions in business flows
- Missing server-side validation (client-side only checks)
- Missing abuse prevention
- Missing entitlement enforcement
- Entitlement bypass through API manipulation

**Common findings:**
- Checkout flow skipping payment verification
- User can complete registration without email verification
- State machine allowing transition from "banned" to "active"
- Race condition allowing double-spending
- Entitlement check only on frontend

**Why it matters:** Business logic bugs don't show up in security scanners. They cause financial loss and require business context to identify.

---

## Incident Response

**Command:** `/launchify-security-incident-response`

**What it checks:**
- No incident response plan
- Missing breach notification procedures
- Missing escalation paths
- Missing incident ownership (no clear owner)
- Missing runbooks for common incidents
- Missing forensic preservation procedures
- Missing post-incident review process
- Missing tabletop exercises

**Common findings:**
- No documented incident response plan
- No clear escalation path for security incidents
- No runbook for data breach
- No process for preserving evidence
- No post-mortem process

**Why it matters:** It's not if you'll have an incident, it's when. Without preparation, incidents become catastrophes.

---

## Feature Readiness

**Command:** `/launchify-security-feature-readiness`

**What it checks:**
- Missing error handling on feature endpoints
- Missing authorization on feature endpoints
- Missing tenant isolation
- Missing retry behavior
- Missing monitoring and alerting
- Missing documentation
- Missing accessibility support
- Missing tests
- Missing deployment configuration

**Common findings:**
- Feature endpoint returns 500 with stack trace
- No authorization check on new feature
- Feature not accessible in staging
- No monitoring on feature usage
- Feature not documented

**Why it matters:** Features that aren't production-ready create support burden, security risk, and user frustration.
