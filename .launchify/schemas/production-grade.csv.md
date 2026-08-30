# Production Grade Report CSV Schema

**Launchify Production Grade Report — Canonical CSV Format**

---

## Columns

| Column | Description |
|---|---|
| Dimension | Dimension name (Security, Reliability, Code Quality, Testing, Infrastructure, Deployment, Monitoring, Feature Completeness, Dependencies, Documentation, Privacy, Operational Readiness) |
| Score | 0-100 score |
| Grade | Letter grade (A+, A, B+, B, B-, C+, C, C-, D, F) |
| Weight | Percentage weight (e.g., 20%, 15%, 10%, 5%) |
| Weighted Score | Score * Weight |
| Finding Count | Number of findings in this dimension |
| Critical Findings | Number of CRITICAL findings |
| High Findings | Number of HIGH findings |
| Medium Findings | Number of MEDIUM findings |
| Low Findings | Number of LOW findings |
| Recommendation | Top recommendation for improvement |

---

## Example Row

```
Security,72,C-,20%,14.4,8,1,2,3,2,Address CRITICAL JWT validation bypass and HIGH IDOR on user endpoints
```
