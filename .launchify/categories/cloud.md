# Cloud Security

**Category ID:** `cloud`

---

## Scope

Inspect all cloud configurations, IAM policies, network settings, storage configurations, metadata endpoint protections, and cloud-specific security controls across AWS, GCP, Azure, and other cloud providers.

---

## Checks

### IAM (Identity and Access Management)
- Overprivileged cloud IAM roles (AWS/GCP/Azure)
- Wildcard actions (`"Action": "*"`) in IAM policies
- Wildcard resources (`"Resource": "*"`) in IAM policies
- Administrator policies attached to workloads
- Shared service accounts across multiple services
- Long-lived access keys (IAM user keys instead of role assumption)
- Missing workload identity (GCP Workload Identity, AWS IAM Roles for Service Accounts)
- Missing least privilege principle
- Excessive cross-account / cross-project / cross-subscription access
- Privileged CI/CD identities with production access
- Privileged developer identities with production access
- Unused IAM roles and stale bindings
- Missing permission boundaries
- Missing separation of duties
- Missing access reviews
- Missing MFA for privileged users
- Cloud credentials available to untrusted workloads
- Service accounts able to modify security controls
- Roles able to read secrets or modify production infrastructure unnecessarily
- IAM policies not version-controlled
- Missing IAM audit logging
- Missing IAM drift detection

### Cloud Service Enumeration
- S3 bucket enumeration through `ListBuckets` or `HeadBucket` error responses
- GCS bucket enumeration through access pattern differences
- Azure Storage enumeration through account name brute-forcing
- Lambda/Cloud Functions enumeration through naming patterns
- Missing error message normalization (different errors for existing vs non-existing resources)
- Cloud service enumeration through response timing differences

### AWS-Specific
- Missing AWS Organizations SCPs restricting actions
- Missing AWS Config rules for compliance
- Missing GuardDuty threat detection
- Missing Macie for S3 sensitive data detection
- Missing Security Hub aggregation
- Missing VPC Flow Logs analysis
- Missing CloudTrail insights
- Missing S3 Block Public Access at account level

### GCP-Specific
- Missing Organization Policy constraints
- Missing Security Command Center
- Missing VPC Service Controls
- Missing Cloud Armor WAF rules
- Missing Binary Authorization for containers
- Missing Confidential Computing for sensitive workloads

### Azure-Specific
- Missing Azure Defender / Microsoft Defender for Cloud
- Missing Azure Policy assignments
- Missing Azure Sentinel/SIEM configuration
- Missing Azure Key Vault access policies
- Missing Azure Private Link for services
- Missing Azure DDoS Protection

### Storage Security
- Public S3 buckets (or equivalent: GCP Storage, Azure Blob)
- Unencrypted storage (missing server-side encryption)
- Missing access logging on storage buckets
- Missing lifecycle policies (old data never cleaned up)
- Public snapshots (RDS, ElastiCache)
- Public EBS volumes
- Missing bucket policies
- Missing object-level permissions
- Storage accessible from untrusted networks
- Missing versioning on critical buckets
- Missing object lock for compliance data

### Networking
- Missing private endpoints for services
- Unrestricted outbound access from workloads
- Publicly accessible databases
- Publicly accessible queues (SQS, RabbitMQ, etc.)
- Publicly accessible admin tools
- Missing network segmentation
- Flat VPC/VNet design (no public/private subnet separation)
- Missing egress controls
- Unrestricted east-west traffic
- Missing service-to-service network policies
- Missing security groups with least privilege
- Missing NACLs or firewall rules
- Missing network flow logs
- Missing DNS security (DNSSEC)

### Compute Security
- Instances with excessive permissions (attached IAM roles)
- Missing instance metadata protections (IMDSv1)
- Public-facing instances without bastion
- Missing IMDSv2 enforcement
- Instances with public IP addresses without justification
- Missing instance hardening
- Missing CIS benchmark compliance
- Missing host-based firewall
- Instances with unnecessary services running

### Cloud Metadata Endpoints
- Exposed cloud metadata endpoints (169.254.169.254)
- SSRF paths to AWS IMDS
- Missing IMDSv2 enforcement
- Metadata access from containers
- Metadata access from serverless functions
- Metadata access from browser-controlled URLs
- Cloud credential theft through metadata services
- Missing metadata endpoint network restrictions
- Workloads with unnecessary metadata access

### Logging and Monitoring
- Missing cloud audit-log collection (CloudTrail, Audit Logs, Activity Log)
- Missing cloud configuration scanning (AWS Config, GCP Config Validator)
- Missing cloud monitoring (CloudWatch, Stackdriver, Azure Monitor)
- Missing access logging on sensitive operations
- Missing alerting on security-relevant events
- Missing log retention policies
- Missing log integrity controls

### Secrets Management
- Secrets stored in environment variables without secret manager
- Secrets in cloud configuration files
- Secrets in Lambda/Azure Functions/Cloud Function environment variables
- Secrets in EC2 user-data
- Missing secret rotation
- Missing secret access auditing
- Excessive secret access permissions
- Secrets copied between environments

---

## Methodology

1. Inspect all IAM roles, policies, and bindings for excessive permissions
2. Check storage bucket permissions and encryption settings
3. Review network configuration for segmentation and private endpoints
4. Verify compute instances have minimal permissions
5. Check cloud audit logging is enabled
6. Verify cloud configuration scanning is in place
7. Inspect cross-account and cross-project access patterns
8. Check for long-lived credentials and access keys
9. Verify workload identity is used where available
10. Review cloud-specific security best practices for the provider
11. Check metadata endpoint protections
12. Verify secret management follows best practices

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Public S3 bucket with sensitive data | CRITICAL |
| IAM role with admin privileges on production workload | CRITICAL |
| Cloud credential theft through metadata endpoint | CRITICAL |
| Missing IMDSv2 enforcement | HIGH |
| Long-lived access keys for CI/CD | HIGH |
| Database publicly accessible | HIGH |
| Missing cloud audit logging | MEDIUM |
| Unused IAM role | LOW |

---

## Evidence Requirements

- Cloud provider and service affected
- Specific IAM policy, storage config, or network rule
- Whether the finding requires cloud API access to confirm
- Impact on data confidentiality, integrity, or availability
- Whether the finding is in infrastructure-as-code or runtime state
