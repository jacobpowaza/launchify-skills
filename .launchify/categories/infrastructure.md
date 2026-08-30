# Infrastructure and Deployment Security

**Category ID:** `infrastructure`

---

## Scope

Inspect all infrastructure-as-code, deployment configurations, container security, Kubernetes security, WAF/API gateway protections, vulnerability scanning, server patching, network segmentation, and infrastructure secrets exposure.

---

## Checks

### Network Segmentation
- Missing network segmentation
- AI services, databases, queues, admin tools all on the same network
- Missing private subnets
- Missing isolation between public, application, data, management, and build networks
- Databases reachable from the public internet
- Queues reachable from untrusted networks
- Administrative interfaces reachable from application networks
- Missing egress controls
- Unrestricted east-west traffic
- Missing service-to-service network policies
- Missing Kubernetes NetworkPolicies
- Flat VPC or VNet design
- Shared security groups with excessive reachability
- Missing bastion or controlled administrative access
- Missing private endpoints
- Unrestricted outbound access from workloads
- Network paths that allow SSRF to reach sensitive services

### Container Security
- Containers running as root
- Privileged containers
- Exposed Docker sockets
- Docker socket mounted into application containers
- Host filesystem mounts
- Host network mode
- Host PID/IPC namespace
- Missing read-only root filesystems
- Missing dropped Linux capabilities / excessive capabilities
- Missing seccomp profiles
- Missing AppArmor or SELinux controls
- Untrusted, unpinned, vulnerable base images
- Secrets baked into images
- Debug tools in production images
- Package managers left in production images
- Missing image signing, provenance, vulnerability scanning
- Containers with unnecessary network/filesystem access
- Writable sensitive paths
- Unsafe entrypoints, unsafe shell execution
- Missing resource and process limits
- Container escape risks
- Insecure registries
- Public container images containing sensitive data

### Kubernetes Security
- Kubernetes misconfiguration
- Open Kubernetes dashboards
- Weak Kubernetes RBAC
- Exposed Kubernetes secrets
- Secrets stored without encryption
- Service accounts with excessive permissions
- Automounted service-account tokens unnecessarily
- Privileged pods
- HostPath mounts
- Host networking
- Host PID/IPC namespace
- Containers running as root
- Missing pod security standards
- Missing admission controls
- Missing NetworkPolicies
- Public API server/kubelet exposure
- Exposed metrics endpoints
- Insecure ingress
- Missing TLS
- Weak TLS configuration
- Missing resource limits
- Missing namespace isolation
- Cross-namespace access
- Unrestricted egress/ingress
- Mutable image tags
- Missing image signature verification
- Missing image scanning
- Exposed Helm values
- Secrets in manifests/ConfigMaps
- Debug pods in production
- Missing audit logging
- Missing control-plane monitoring
- Missing backup/restore testing
- Unsafe operators
- Excessive CRD permissions
- Unrestricted exec access
- Unrestricted port forwarding

### WAF and API Gateway Protections
- Missing WAF protections
- Missing API gateway protections
- Direct exposure of backend services
- Missing centralized authentication
- Missing centralized rate limiting
- Missing centralized request validation
- Missing bot protection
- Missing DDoS protections
- Missing request-size limits
- Missing schema enforcement
- Missing API version controls
- Missing threat detection
- Missing gateway logging
- Gateway checks that fail open
- Inconsistent protections between routes
- Bypass paths that reach services directly

### Vulnerability Scanning and Security Tooling
- No SAST in CI/CD
- No DAST in pipeline
- No dependency scanning
- No container scanning
- No infrastructure-as-code scanning
- No secrets scanning
- No SBOM generation
- No license/supply-chain review
- Security scans not running on pull requests
- Security scans not running before deployment
- Security scan failures ignored
- Missing vulnerability triage
- Missing remediation SLAs
- Missing exception tracking
- Missing scan-result retention
- Missing runtime vulnerability monitoring
- Missing cloud configuration scanning
- Missing Kubernetes scanning
- Missing image provenance verification

### Server Patching
- Unpatched servers
- Unpatched operating systems
- Unpatched container hosts
- Unpatched Kubernetes nodes
- Unpatched managed services
- Unpatched runtime versions
- Unsupported operating systems
- Unsupported language runtimes
- Missing patch schedules
- Missing emergency patch process
- Missing patch verification
- Missing asset inventory
- Unknown internet-facing servers
- Stale machine images/AMIs
- Unpatched development or staging environments that can access production

### Infrastructure Secrets Exposure
- Terraform state files containing secrets
- Kubernetes secrets exposed in repositories or logs
- CI variables exposed in logs or artifacts
- Secrets in Helm charts
- Secrets in cloud-init scripts
- Secrets in user-data
- Secrets in machine images
- Secrets in Terraform plans/outputs
- Secrets in deployment manifests
- Secrets in GitHub Actions, GitLab CI, Jenkins
- Secrets in build caches
- Secrets in container registries
- Secrets in monitoring systems
- Secrets in backups
- Missing secret-manager integration
- Missing secret rotation
- Missing secret access auditing
- Excessive secret access
- Secrets copied between environments

---

## Methodology

1. Read `.launchify/checks/infrastructure.md` for the full checklist
2. Inspect infrastructure-as-code files (Terraform, CloudFormation, Pulumi)
3. Inspect Kubernetes manifests, Helm charts, Kustomize configurations
4. Inspect Dockerfiles and container configurations
5. Inspect CI/CD pipelines for infrastructure-related security
6. Inspect WAF and API gateway configurations
7. Verify vulnerability scanning is in place and operational
8. Verify server patching processes exist
9. Check for infrastructure secrets exposure
10. Verify deployment safety controls
11. Check network segmentation
12. Verify container security best practices

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Privileged container in production | CRITICAL |
| Kubernetes secrets in plaintext | CRITICAL |
| Missing Kubernetes NetworkPolicy | HIGH |
| Exposed Kubernetes dashboard | HIGH |
| Containers running as root | MEDIUM |
| Missing image vulnerability scanning | MEDIUM |
| Unpinned container base image | LOW |
| Exposed Docker socket | CRITICAL |

---

## Evidence Requirements

- Infrastructure technology and provider
- Specific resource, manifest, or configuration affected
- Whether the finding is in code or runtime state
- Whether runtime validation is needed to confirm
- Impact on confidentiality, integrity, or availability
