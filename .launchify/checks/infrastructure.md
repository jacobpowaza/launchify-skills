# Infrastructure and Deployment Checks

**Launchify Infrastructure & Deployment Security Checks — Canonical Reference**

---

## Network Segmentation

Check for:
- Missing network segmentation
- AI services, databases, queues, admin tools, and public-facing services on the same network
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

---

## Cloud IAM

Check for:
- Overprivileged cloud IAM (AWS, GCP, Azure)
- Wildcard actions and wildcard resources
- Administrator policies attached to workloads
- Shared service accounts
- Long-lived access keys
- Missing workload identity
- Missing least privilege
- Excessive cross-account, cross-project, cross-subscription access
- Privileged CI/CD identities
- Privileged developer identities
- Unused IAM roles
- Stale IAM bindings
- Missing permission boundaries
- Missing separation of duties
- Missing access reviews
- Missing MFA for privileged users
- Cloud credentials available to untrusted workloads
- Service accounts able to modify security controls
- Roles able to read secrets or modify production infrastructure unnecessarily

---

## Cloud Metadata Endpoints

Check for:
- Exposed cloud metadata endpoints (169.254.169.254)
- SSRF paths to AWS IMDS
- Missing IMDSv2 enforcement
- Metadata access from containers, serverless functions, browser-controlled URLs
- Cloud credential theft through metadata services
- Missing metadata endpoint network restrictions
- Workloads with unnecessary metadata access

---

## Container Security

Check for:
- Containers running as root
- Privileged containers
- Exposed Docker sockets
- Docker socket mounted into application containers
- Host filesystem mounts, host network mode, host PID/IPC namespace
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

---

## Kubernetes Security

Check for:
- Kubernetes misconfiguration
- Open Kubernetes dashboards
- Weak Kubernetes RBAC
- Exposed Kubernetes secrets
- Secrets stored without encryption
- Service accounts with excessive permissions
- Automounted service-account tokens unnecessarily
- Privileged pods, HostPath mounts, host networking, host PID/IPC
- Containers running as root
- Missing pod security standards, admission controls, NetworkPolicies
- Public API server/kubelet exposure
- Exposed metrics endpoints
- Insecure ingress, missing TLS, weak TLS
- Missing resource limits, namespace isolation
- Cross-namespace access, unrestricted egress/ingress
- Mutable image tags, missing image signature verification, missing image scanning
- Exposed Helm values, secrets in manifests/ConfigMaps
- Debug pods in production
- Missing audit logging, control-plane monitoring, backup/restore testing
- Unsafe operators, excessive CRD permissions
- Unrestricted exec access, unrestricted port forwarding

---

## WAF and API Gateway Protections

Check for:
- Missing WAF protections
- Missing API gateway protections
- Direct exposure of backend services
- Missing centralized authentication, rate limiting, request validation
- Missing bot protection, DDoS protections
- Missing request-size limits, schema enforcement, API version controls
- Missing threat detection, gateway logging
- Gateway checks that fail open
- Inconsistent protections between routes
- Bypass paths that reach services directly

---

## Vulnerability Scanning and Security Tooling

Check for:
- No SAST, DAST, dependency scanning, container scanning
- No infrastructure-as-code scanning, secrets scanning
- No SBOM generation, license/supply-chain review
- Security scans not running on pull requests or before deployment
- Security scan failures ignored
- Missing vulnerability triage, remediation SLAs
- Missing exception tracking, scan-result retention
- Missing runtime vulnerability monitoring
- Missing cloud configuration scanning, Kubernetes scanning
- Missing image provenance verification

---

## Server Patching

Check for:
- Unpatched servers, operating systems, container hosts, Kubernetes nodes
- Unpatched managed services, runtime versions
- Unsupported operating systems, language runtimes
- Missing patch schedules, emergency patch process, patch verification
- Missing asset inventory
- Unknown internet-facing servers
- Stale machine images, AMIs
- Unpatched development or staging environments that can access production

---

## Infrastructure Secrets Exposure

Check for:
- Terraform state files containing secrets
- Kubernetes secrets exposed in repositories or logs
- CI variables exposed in logs or artifacts
- Secrets in Helm charts, cloud-init scripts, user-data, machine images
- Secrets in Terraform plans/outputs, deployment manifests
- Secrets in GitHub Actions, GitLab CI, Jenkins, or other CI systems
- Secrets in build caches, container registries, monitoring systems, backups
- Missing secret-manager integration, secret rotation, secret access auditing
- Excessive secret access
- Secrets copied between environments

---

## Deployment Safety

Check for:
- Insecure deployment defaults
- Production deployment without review or rollback
- Missing blue-green or canary controls where required
- Missing health, readiness, liveness checks
- Missing graceful shutdown
- Missing migration coordination
- Deployment order failures
- Configuration drift
- Environment parity failures
- Staging not representative of production
- Missing deployment audit logs
- Missing artifact integrity verification
- Unsigned artifacts, mutable deployment artifacts
- Unpinned images, unpinned build dependencies
- Deployment credentials with excessive permissions
- Direct production access from developer machines
- Missing break-glass controls
- Missing disaster recovery deployment procedure
- Missing infrastructure drift detection
- Missing rollback testing
