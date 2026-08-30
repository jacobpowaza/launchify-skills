# Secrets & Configuration Security

**Category ID:** `secrets`

---

## Scope

Inspect all secrets, credentials, configuration values, and sensitive data across the repository, infrastructure, deployment, CI/CD, and runtime environments. No secret should reach an untrusted party through source code, build artifacts, logs, infrastructure, version control, client bundles, or runtime exposure.

---

## Checks

### Source Code Secrets
- Hardcoded API keys, tokens, passwords, connection strings in source code
- Hardcoded AWS access keys and secret keys
- Hardcoded GCP service account keys or JSON key files
- Hardcoded Azure storage account keys or connection strings
- Hardcoded database credentials (Postgres, MySQL, MongoDB, Redis, etc.)
- Hardcoded Redis, Memcached, or other cache credentials
- Hardcoded SMTP credentials
- Hardcoded payment provider keys (Stripe, PayPal, Braintree, etc.)
- Hardcoded JWT signing secrets
- Hardcoded encryption keys or initialization vectors
- Hardcoded OAuth client secrets
- Hardcoded session secrets
- Hardcoded Sentry DSNs with embedded keys
- Hardcoded webhook signing secrets
- Hardcoded API gateway keys
- Hardcoded third-party service credentials (Twilio, SendGrid, Algolia, etc.)

### Environment and Configuration Files
- Public `.env` files committed to the repository
- `.env` files not in `.gitignore`
- `.env.local`, `.env.production`, `.env.staging` files committed
- `.env.example` containing real (not placeholder) credentials
- Configuration files with embedded secrets (config.yaml, config.json, settings.py, etc.)
- Docker Compose files with plaintext database passwords
- Application configuration files with production credentials
- Feature flag files containing service credentials
- YAML/JSON/TOML configuration with embedded secrets

### Version Control Exposure
- Secrets in Git history (even if removed from current files)
- Secrets in Git commit messages
- Secrets in Git stash entries
- Secrets in branches that were deleted but accessible via reflog
- Secrets in Git tags
- Secrets in `.git/config` or `.gitmodules`
- Pre-commit hooks not scanning for secrets

### Build Artifacts and Bundles
- Secrets leaked in frontend JavaScript bundles
- Secrets in compiled binaries
- Secrets in source maps
- Secrets in build output directories (dist/, build/, out/)
- Secrets in webpack, Vite, Rollup, or other bundler output
- Secrets in CSS bundles
- Secrets in inline scripts in HTML templates
- Secrets in Next.js `__NEXT_DATA__` script tags
- Secrets in Nuxt `__NUXT__` script tags

### Container and Image Secrets
- Secrets baked into Docker images
- Secrets in Dockerfile RUN commands
- Secrets in Docker layer history
- Secrets in Docker Compose environment sections
- Secrets in `.docker/config.json`
- Secrets in container entrypoint scripts
- Secrets in container health check commands
- Debug tools left in production images

### Infrastructure and Cloud Secrets
- Secrets in Terraform state files
- Secrets in Terraform variables without sensitive marking
- Secrets in Terraform outputs
- Secrets in CloudFormation templates
- Secrets in Pulumi code
- Secrets in Ansible playbooks and vault files
- Secrets in Packer templates
- Secrets in Kubernetes manifests (not using Secrets resource)
- Secrets in Helm values files
- Secrets in Kubernetes ConfigMaps
- Secrets stored as base64-encoded Kubernetes Secrets (not encrypted)
- Secrets in cloud-init scripts
- Secrets in EC2 user-data
- Secrets in GCP startup scripts
- Secrets in Azure custom data
- Secrets in Lambda environment variables (visible in console)
- Secrets in ECS task definitions
- Secrets in Cloud Run configurations

### CI/CD Secrets
- Secrets exposed in CI/CD logs
- Secrets in GitHub Actions workflow files
- Secrets in GitLab CI `.gitlab-ci.yml`
- Secrets in Jenkins pipeline files
- Secrets in CircleCI configuration
- Secrets in Travis CI configuration
- Secrets in buildkite pipeline files
- Secrets printed to stdout/stderr in CI steps
- Secrets in CI artifact uploads
- Secrets in CI cache entries
- Secrets in CI test output
- Secrets in CI coverage reports
- Secrets in deployment scripts called from CI

### Runtime and Service Exposure
- Verbose production error messages leaking secrets
- Stack traces exposing environment variables
- Debug endpoints exposing configuration
- Health check endpoints exposing internal URLs and credentials
- Metrics endpoints exposing service credentials
- Admin dashboards exposed without authentication
- Logs containing secrets (API keys, tokens, passwords)
- Crash reports containing environment variables
- APM tools capturing request bodies with secrets
- Error tracking services (Sentry, Bugsnag) capturing secrets in breadcrumbs
- Profiling tools exposing environment data

### Client-Side and Frontend Secrets
- Firebase API keys in frontend code
- Supabase keys exposed inappropriately
- AWS Amplify configuration in frontend bundles
- Google Maps API keys in frontend code
- Stripe publishable keys (acceptable) vs. secret keys (not acceptable)
- Sentry DSN with embedded secrets
- Analytics tokens in frontend code
- Feature flags containing service credentials
- Service worker code containing secrets
- Browser extension API keys

### Default Credentials
- Default database passwords (postgres/postgres, root/root, admin/admin)
- Default admin panel credentials
- Default API credentials on services (RabbitMQ, Elasticsearch, etc.)
- Default SSH keys in container images
- Default TLS certificates and private keys
- Default JWT secrets in framework configurations
- Default session secrets in framework configurations
- Default encryption keys in framework configurations

### Cryptographic Failures
- TLS 1.0 or 1.1 enabled (should require TLS 1.2+)
- Weak cipher suites (RC4, DES, 3DES, NULL, EXPORT)
- Weak hash algorithms in non-password contexts (MD5 for file integrity, SHA1 for certificates)
- Missing certificate transparency logging
- Self-signed certificates in production
- Expired TLS certificates
- Missing OCSP stapling
- RSA keys < 2048 bits
- ECDSA keys < 256 bits
- Missing certificate pinning for critical services
- Weak key exchange algorithms
- Missing HSTS with long max-age

### Secret Management
- Missing secret management system (Vault, AWS Secrets Manager, etc.)
- Secrets not rotated since initial deployment
- Same secret used across multiple environments
- Same secret shared across multiple services
- Secrets accessible to too many services or roles
- Missing secret access auditing
- Missing secret rotation policies
- Missing secret expiration
- Secrets passed as command-line arguments (visible in process list)
- Secrets in environment variables accessible to child processes

---

## Methodology

1. Search all source files for hardcoded secrets, API keys, tokens, passwords using pattern matching and entropy analysis
2. Search `.env` files, `.env.*` files, and configuration files for exposed credentials
3. Search Git history for committed secrets using `git log -p` and secret scanning tools
4. Search frontend bundles and source maps for embedded secrets
5. Search infrastructure-as-code for secret values in plaintext
6. Search CI/CD configuration for exposed secrets in logs and artifacts
7. Search container images and Dockerfiles for baked-in secrets
8. Search Kubernetes manifests for plain-text secrets
9. Verify `.gitignore` includes all secret-containing files
10. Check default credentials for all services and frameworks in use
11. Verify secret rotation policies exist
12. Verify secrets are not passed through untrusted AI tools or external services
13. Check for secrets in crash reports, error tracking, and APM tools
14. Verify stack traces do not expose environment variables in production

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Hardcoded production database password in source | CRITICAL |
| API key in frontend bundle | CRITICAL |
| AWS secret key in source code | CRITICAL |
| Secrets in Git history (active repo) | HIGH |
| Secrets in Terraform state (remote backend) | HIGH |
| Default credentials on production service | HIGH |
| Secrets in CI/CD logs | HIGH |
| `.env` file committed but in `.gitignore` | MEDIUM |
| Default credentials in non-production config | MEDIUM |
| Verbose error messages in production | LOW |
| Secrets in crash reports | MEDIUM |

---

## Evidence Requirements

- Exact file and line where secret is found
- Type of secret (database password, API key, token, etc.)
- Whether the secret is in active code, Git history, build artifacts, or infrastructure
- Whether the secret is accessible to untrusted parties
- Whether the secret has been rotated since exposure
- Which environments use this secret
- How many services or roles have access to this secret
