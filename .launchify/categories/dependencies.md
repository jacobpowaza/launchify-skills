# Dependency and Supply-Chain Security

**Category ID:** `dependencies`

---

## Scope

Inspect all dependencies, package manifests, lockfiles, transitive dependencies, and supply-chain security controls. Dependencies are the most common vector for supply chain attacks.

---

## Checks

### Vulnerable Dependencies
- Vulnerable dependencies (known CVEs)
- Outdated dependencies with known vulnerabilities
- Abandoned packages (no maintainer)
- Packages with known malicious maintainers or releases
- Transitive dependencies with vulnerabilities
- Dependencies with critical severity CVEs
- Dependencies with high severity CVEs
- Dependencies with known exploit code available

### Install Script Risk
- `postinstall`/`preinstall` scripts in dependencies that execute arbitrary code
- `prepare` scripts in dependencies executing during install
- `node-gyp` build scripts executing arbitrary code
- `setup.py`/`pyproject.toml` install hooks executing arbitrary code
- Rust `build.rs` scripts executing arbitrary code
- Missing `.npmignore` or `MANIFEST.in` allowing sensitive files into published packages
- Missing `publishConfig` restricting where packages can be published
- Go module replace directives pointing to external repositories
- Private package scope not claimed on public registries (npm, PyPI, Cargo)
- `.npmrc` or `pip.conf` not configured to prefer private registry
- Missing signature verification for downloaded packages
- Package registry not pinned (using public instead of private/mirror)
- Missing provenance attestation for built artifacts

### Supply Chain
- Malicious packages (typosquatting, dependency confusion)
- Unpinned dependencies (no version constraint)
- Untrusted build actions
- Compromised CI/CD dependencies
- Dependency confusion (private package name collision with public)
- Typosquatting (package names similar to popular packages)
- Install-script risk (postinstall scripts in dependencies)
- Build-time code execution
- Runtime package installation
- Untrusted plugins
- Unverified container images
- Malicious npm/pip/cargo packages
- Compromised package maintainer accounts
- Backdoored dependencies

### Verification
- Missing dependency scanning in CI/CD
- Missing SCA (Software Composition Analysis)
- Missing SBOM generation
- Missing lockfiles (package-lock.json, yarn.lock, go.sum, Cargo.lock)
- Lockfile drift (lockfile doesn't match manifest)
- Multiple conflicting versions
- Unsigned artifacts where appropriate
- Unverified package registries
- Missing provenance attestations
- Missing dependency update monitoring
- Missing Dependabot/Renovate configuration
- Missing license compliance checking

### Integration Risks
- Unsafe third-party integrations
- Malicious AI models
- Compromised model downloads
- Unreviewed transitive dependencies
- Dependencies with excessive permissions
- Dependencies with unnecessary capabilities

---

## Methodology

1. Inspect all package manifests (package.json, requirements.txt, go.mod, Cargo.toml, etc.)
2. Run dependency auditing tools (npm audit, cargo audit, pip audit)
3. Check for known vulnerabilities in dependencies
4. Verify lockfiles exist and are consistent with manifests
5. Check for unpinned dependencies
6. Inspect transitive dependencies for risks
7. Check for malicious packages or typosquatting
8. Verify dependency scanning is in CI/CD pipeline
9. Check for SBOM generation
10. Verify container base images are from trusted sources
11. Check for dependency update automation
12. Verify license compliance

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Known critical vulnerability in dependency | CRITICAL |
| Malicious dependency discovered | CRITICAL |
| Dependency confusion attack vector | HIGH |
| Unpinned dependencies in production | MEDIUM |
| Missing SBOM generation | LOW |
| Outdated but non-vulnerable dependency | INFO |

---

## Evidence Requirements

- Package name and version affected
- Vulnerability identifier (CVE, etc.) if available
- Whether the dependency is used in production code
- Whether the vulnerability is exploitable in this context
- Transitive vs direct dependency
