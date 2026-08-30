# Data Protection and Privacy

**Category ID:** `privacy`

---

## Scope

Inspect all data protection, privacy controls, PII handling, data retention, and privacy compliance mechanisms.

---

## Checks

### Data Exposure
- Sensitive information leakage
- Excessive collection
- PII overcollection
- PII exposure
- Sensitive fields unmasked
- Password hashes exposed
- Social Security numbers exposed
- API keys exposed
- Tokens exposed
- Unauthorized analytics
- Sensitive data in search indexes, vector databases, caches, browser storage, logs, error reports
- Sensitive data sent to AI providers

### Encryption
- Unencrypted personal data
- Missing encryption at rest
- Missing encryption in transit
- Missing field-level encryption where required
- Missing data masking

### Retention and Deletion
- Missing retention policies
- Broken data retention policies
- Missing deletion workflows
- No data deletion workflow
- Deleted data remaining in backups without policy
- Missing deletion propagation

### Consent and Rights
- Missing consent management
- Missing purpose limitation
- Missing data-access audit logs
- Missing subject-access workflows
- Missing correction workflows
- Missing export workflows

### Third-Party and Sharing
- Privacy-policy mismatch
- Third-party sharing risks
- Sensitive data copied into telemetry
- Test or staging use of production data

### Classification and Ownership
- Missing data classification
- Missing data ownership
- Missing privacy review for new features

---

## Methodology

1. Identify all PII and sensitive data in the system
2. Trace where PII is collected, stored, processed, and transmitted
3. Verify encryption at rest and in transit
4. Check data retention policies and enforcement
5. Verify deletion workflows work correctly
6. Check consent management and data rights
7. Verify data masking in non-production environments
8. Check third-party data sharing agreements
9. Verify data classification and ownership
10. Check for privacy review in feature development

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| PII in plaintext in database | CRITICAL |
| Missing encryption for sensitive data | HIGH |
| No data deletion workflow | HIGH |
| PII in logs | HIGH |
| Missing consent management | MEDIUM |
| Privacy policy mismatch | MEDIUM |

---

## Evidence Requirements

- Data type and sensitivity level affected
- Where the data is stored and processed
- Whether encryption and access controls are enforced
- Whether deletion and retention policies are in place
- Regulatory implications (GDPR, CCPA, etc.)
