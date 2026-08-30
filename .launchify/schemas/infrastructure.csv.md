# Infrastructure and Deployment Report CSV Schema

**Launchify Infrastructure & Deployment Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| ID | Unique finding identifier (e.g., `INF-001`) |
| Category | Infrastructure category (e.g., `network`, `iam`, `container`, `kubernetes`, `deployment`) |
| Severity | `CRITICAL`, `HIGH`, `MEDIUM`, `LOW`, `INFO` |
| Confidence | `CONFIRMED`, `HIGH`, `MEDIUM`, `LOW`, `NEEDS_RUNTIME_VALIDATION` |
| Resource | Affected infrastructure resource (e.g., `aws_s3_bucket.main`, `k8s_deployment.api`) |
| Environment | Affected environment (`production`, `staging`, `development`, `all`) |
| File | Affected infrastructure-as-code file |
| Location | Line number or range |
| Finding | Brief description of the finding |
| Evidence | Supporting evidence from infrastructure code |
| Exposure | How the resource is exposed (public, private, internal) |
| Impact | Business and technical impact |
| Recommendation | Recommended remediation action |
| Status | `OPEN`, `FIXED`, `WONT_FIX`, `DEFERRED` |
| Runtime Validation | `YES` or `NO` — whether runtime/cloud access is needed |
| Verification | How to verify the fix |

---

## Example Row

```
INF-001,iam,HIGH,NEEDS_RUNTIME_VALIDATION,aws_iam_role.app,production,infra/main.tf,45,IAM role has wildcard S3 permissions,"Action: s3:* Resource: *",Role is attached to application workload,Application can access any S3 bucket in the account,Apply least-privilege S3 permissions to only required buckets,OPEN,YES,Verify application still functions with restricted permissions
```
