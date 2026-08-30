# Cloud Security

**Category ID:** `cloud`

---

## Scope

Inspect all cloud configurations, IAM policies, network settings, storage configurations, and cloud-specific security controls across AWS, GCP, Azure, and other cloud providers.

---

## Checks

### IAM
- Overprivileged cloud IAM
- Wildcard actions and resources
- Administrator policies attached to workloads
- Shared service accounts
- Long-lived access keys
- Missing workload identity
- Missing least privilege
- Excessive cross-account/project/subscription access
- Privileged CI/CD and developer identities
- Unused IAM roles and stale bindings
- Missing permission boundaries and separation of duties
- Missing access reviews and MFA for privileged users
- Cloud credentials available to untrusted workloads

### Storage
- Public S3 buckets or equivalent
- Unencrypted storage
- Missing access logging on storage
- Missing lifecycle policies
- Public snapshots

### Networking
- Missing private endpoints
- Unrestricted outbound access
- Publicly accessible databases, queues, admin tools
- Missing network segmentation
- Flat VPC/VNet design
- Missing egress controls

### Compute
- Instances with excessive permissions
- Missing instance metadata protections
- Public-facing instances without bastion
- Missing IMDSv2 enforcement

### Logging and Monitoring
- Missing cloud audit-log collection
- Missing cloud configuration scanning
- Missing cloud monitoring

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

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Public S3 bucket with sensitive data | CRITICAL |
| IAM role with admin privileges on production workload | CRITICAL |
| Missing IMDSv2 enforcement | HIGH |
| Long-lived access keys for CI/CD | HIGH |
| Missing cloud audit logging | MEDIUM |
| Unused IAM role | LOW |

---

## Evidence Requirements

- Cloud provider and service affected
- Specific IAM policy, storage config, or network rule
- Whether the finding requires cloud API access to confirm
- Impact on data confidentiality, integrity, or availability
- Whether the finding is in infrastructure-as-code or runtime state
