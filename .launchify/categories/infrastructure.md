# Infrastructure and Deployment Security

**Category ID:** `infrastructure`

---

## Scope

Inspect all infrastructure-as-code, deployment configurations, container security, Kubernetes security, WAF/API gateway protections, vulnerability scanning, server patching, and infrastructure secrets exposure.

This is the master infrastructure category. Specific sub-areas are detailed in `.launchify/checks/infrastructure.md`.

---

## Checks

See `.launchify/checks/infrastructure.md` for the complete infrastructure and deployment security checklist covering:
- Network segmentation
- Cloud IAM
- Cloud metadata endpoints
- Container security
- Kubernetes security
- WAF and API gateway protections
- Vulnerability scanning and security tooling
- Server patching
- Infrastructure secrets exposure
- Deployment safety

---

## Methodology

1. Read `.launchify/checks/infrastructure.md` for the full checklist
2. Inspect infrastructure-as-code files (Terraform, CloudFormation, Pulumi, etc.)
3. Inspect Kubernetes manifests, Helm charts, and Kustomize configurations
4. Inspect Dockerfiles and container configurations
5. Inspect CI/CD pipelines for infrastructure-related security
6. Inspect WAF and API gateway configurations
7. Verify vulnerability scanning is in place and operational
8. Verify server patching processes exist
9. Check for infrastructure secrets exposure
10. Verify deployment safety controls

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Privileged container in production | CRITICAL |
| Missing Kubernetes NetworkPolicy | HIGH |
| Exposed Kubernetes dashboard | HIGH |
| Containers running as root | MEDIUM |
| Missing image vulnerability scanning | MEDIUM |
| Unpinned container base image | LOW |

---

## Evidence Requirements

- Infrastructure technology and provider
- Specific resource, manifest, or configuration affected
- Whether the finding is in code or runtime state
- Whether runtime validation is needed to confirm
- Impact on confidentiality, integrity, or availability
