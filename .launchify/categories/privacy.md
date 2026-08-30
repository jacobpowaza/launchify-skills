# Data Protection and Privacy

**Category ID:** `privacy`

---

## Scope

Inspect all data protection, privacy controls, PII handling, encryption, data retention, deletion workflows, consent management, and privacy compliance mechanisms. Privacy violations cause regulatory fines and user trust erosion.

---

## Checks

### Data Exposure
- PII overcollection (collecting more data than needed)
- Sensitive information leakage through API responses
- PII exposure in logs, error messages, analytics
- Sensitive fields unmasked (password hashes, SSNs, API keys, tokens)
- Password hashes exposed in API responses
- Social Security numbers stored unencrypted
- API keys stored in plaintext
- Tokens stored in plaintext
- Credit card data stored without PCI compliance
- Health data stored without HIPAA compliance
- Unauthorized analytics collecting PII
- Sensitive data in search indexes
- Sensitive data in vector databases
- Sensitive data in caches
- Sensitive data in browser storage
- Sensitive data in logs
- Sensitive data in error reports
- Sensitive data sent to AI providers
- Sensitive data in telemetry
- Sensitive data in third-party services

### Cryptographic Key Management
- Missing key management system (KMS)
- Encryption keys hardcoded in source
- Missing envelope encryption for cloud KMS
- Encryption key access not audited
- Missing customer-managed encryption keys (CMEK) where required
- Missing key rotation schedule
- Missing key versioning
- Missing key access separation (encryption vs decryption keys)

### Encryption
- Unencrypted personal data at rest
- Missing encryption at rest for sensitive data
- Missing encryption in transit (HTTP instead of HTTPS)
- Missing field-level encryption for highly sensitive data
- Missing data masking in non-production environments
- Sensitive data copied into development or staging without masking
- Weak encryption algorithms (DES, 3DES, MD5 for passwords)
- Missing key management
- Encryption keys hardcoded in source
- Missing TLS for internal services

### Retention and Deletion
- Missing retention policies
- Broken data retention policies (data retained longer than policy states)
- Missing deletion workflows (right to be forgotten)
- No data deletion workflow
- Deleted data remaining in backups without policy
- Missing deletion propagation (data deleted from primary but remains in cache, search index, vector DB)
- Missing automated deletion
- Missing deletion verification
- Missing backup rotation
- Data retained indefinitely without justification

### Consent and Rights
- Missing consent management
- Missing purpose limitation (data used beyond original purpose)
- Missing data-access audit logs
- Missing subject-access workflows (user requesting their data)
- Missing correction workflows (user correcting their data)
- Missing export workflows (user downloading their data)
- Missing consent withdrawal mechanism
- Missing consent records
- Missing privacy settings for users

### Third-Party and Sharing
- Privacy-policy mismatch (policy says one thing, code does another)
- Third-party sharing risks (data shared with partners without consent)
- Sensitive data copied into telemetry
- Test or staging use of production data
- Data shared with AI providers without user consent
- Data shared with analytics without user consent
- Missing data processing agreements
- Missing data residency compliance

### Classification and Ownership
- Missing data classification (no labeling of sensitive data)
- Missing data ownership (no clear owner for sensitive data)
- Missing privacy review for new features
- Missing privacy impact assessments
- Missing data protection officer
- Missing breach notification process
- Missing regulatory compliance documentation

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
11. Verify deletion propagation across all systems
12. Check for PII in logs and error messages
13. Verify data minimization principles
14. Check for privacy impact assessments

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| PII in plaintext in database | CRITICAL |
| Missing encryption for sensitive data | HIGH |
| No data deletion workflow | HIGH |
| PII in logs | HIGH |
| Sensitive data sent to AI provider without consent | HIGH |
| Privacy policy mismatch | MEDIUM |
| Missing consent management | MEDIUM |
| Missing data classification | LOW |
| Sensitive data in staging without masking | MEDIUM |

---

## Evidence Requirements

- Data type and sensitivity level affected
- Where the data is stored and processed
- Whether encryption and access controls are enforced
- Whether deletion and retention policies are in place
- Regulatory implications (GDPR, CCPA, HIPAA, PCI-DSS)
- Whether the data is shared with third parties
