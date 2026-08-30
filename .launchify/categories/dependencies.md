# Dependency and Supply-Chain Security

**Category ID:** `dependencies`

---

## Scope

Inspect all dependencies, package manifests, lockfiles, transitive dependencies, and supply-chain security controls.

---

## Checks

### Vulnerable Dependencies
- Vulnerable dependencies
- Outdated dependencies
- Abandoned packages
- Packages with known malicious maintainers or releases

### Supply Chain
- Malicious packages
- Unpinned dependencies
- Untrusted build actions
- Compromised CI/CD dependencies
- Dependency confusion
- Typosquatting
- Install-script risk
- Build-time code execution
- Runtime package installation
- Untrusted plugins
- Unverified container images

### Verification
- Missing dependency scanning
- Missing SCA (Software Composition Analysis)
- Missing SBOM generation
- Missing lockfiles
- Lockfile drift
- Multiple conflicting versions
- Unsigned artifacts where appropriate
- Unverified package registries
- Missing provenance attestations
- Missing dependency update monitoring

### Integration Risks
- Unsafe third-party integrations
- Malicious AI models
- Compromised model downloads
- Unreviewed transitive dependencies

---

## Methodology

1. Inspect all package manifests (package.json, requirements.txt, go.mod, Cargo.toml, etc.)
2. Run dependency auditing tools
3. Check for known vulnerabilities in dependencies
4. Verify lockfiles exist and are consistent with manifests
5. Check for unpinned dependencies
6. Inspect transitive dependencies for risks
7. Check for malicious packages or typosquatting
8. Verify dependency scanning is in CI/CD pipeline
9. Check for SBOM generation
10. Verify container base images are from trusted sources

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
