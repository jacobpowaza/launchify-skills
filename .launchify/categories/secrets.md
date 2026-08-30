# Secrets & Configuration Security

**Category ID:** `secrets`

---

## Scope

Inspect all secrets, credentials, configuration values, and sensitive data across the repository, infrastructure, deployment, CI/CD, and runtime environments.

---

## Checks

### Exposed Credentials
- Exposed database credentials
- Public `.env` files
- Hardcoded secrets in source code
- Secrets committed to Git history
- Default credentials

### Secrets in Artifacts
- Secrets leaked in frontend JavaScript bundles
- Secrets stored in client-side storage
- Secrets in source maps
- Secrets in build artifacts
- Secrets in crash reports
- Secrets in container logs
- Secrets in backup files

### Cloud and Infrastructure Secrets
- Exposed API keys
- Exposed cloud credentials
- Exposed CI/CD secrets
- Terraform state file leaks
- Kubernetes secret exposure
- Secrets in Helm values
- Secrets in Docker images or layers
- Secrets in infrastructure outputs
- Secrets in GitHub Actions, GitLab CI, Jenkins, or other CI systems
- Secrets in build caches
- Secrets in container registries
- Secrets in monitoring systems
- Secrets in infrastructure backups

### Configuration Exposure
- Exposed production configuration
- Exposed staging or development environments
- Production debug tools enabled
- Verbose production errors
- Logs leaking secrets
- Configuration drift between environments
- Secrets passed to untrusted AI tools
- Secrets exposed through environment inspection
- Secrets included in client-side feature configuration
- Backup files publicly accessible

---

## Methodology

1. Search all source files for hardcoded secrets, API keys, tokens, passwords
2. Search `.env` files, `.env.*` files, and configuration files for exposed credentials
3. Search Git history for committed secrets
4. Search frontend bundles and source maps for embedded secrets
5. Search infrastructure-as-code for secret values
6. Search CI/CD configuration for exposed secrets
7. Search container images and Dockerfiles for baked-in secrets
8. Search Kubernetes manifests for plain-text secrets
9. Verify `.gitignore` includes all secret-containing files
10. Verify secrets are not passed through untrusted AI tools or external services

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Hardcoded production database password in source | CRITICAL |
| API key in frontend bundle | CRITICAL |
| Secrets in Git history (active repo) | HIGH |
| Secrets in Terraform state (remote backend) | HIGH |
| `.env` file committed but in `.gitignore` | MEDIUM |
| Default credentials in non-production config | MEDIUM |
| Verbose error messages in production | LOW |

---

## Evidence Requirements

- Exact file and line where secret is found
- Type of secret (database password, API key, token, etc.)
- Whether the secret is in active code, Git history, build artifacts, or infrastructure
- Whether the secret is accessible to untrusted parties
- Whether the secret has been rotated since exposure
