# Legal Policies, Compliance Documents & Regulatory Requirements for Software Products

> **Research Date:** August 2026
> **Scope:** SaaS, web apps, mobile apps
> **Jurisdiction:** Global (GDPR), United States (federal + 20 state privacy laws)

---

## Table of Contents

1. [Complete Policy Inventory](#1-complete-policy-inventory)
2. [Jurisdictional Requirements Map](#2-jurisdictional-requirements-map)
3. [Investor & Enterprise Customer Requirements](#3-investor--enterprise-customer-requirements)
4. [Minimum Viable Policy Set for Startups](#4-minimum-viable-policy-set-for-startups)
5. [Automated Compliance Checks](#5-automated-compliance-checks)
6. [Consequences of Non-Compliance](#6-consequences-of-non-compliance)

---

## 1. Complete Policy Inventory

### TIER 1: CRITICAL — Legally Required (Lawsuit/Fine Risk if Missing)

#### 1.1 Privacy Policy / Privacy Notice

| Attribute | Detail |
|---|---|
| **Why Required** | Legally mandated by GDPR (Art. 12-14), CCPA/CPRA, all 20 US state privacy laws, COPPA, app store policies (Apple/Google), payment processors (Stripe), and LGPD (Brazil) |
| **Penalty if Missing** | GDPR: up to €20M or 4% annual revenue. CCPA: $2,500/violation (negligent), $7,500/violation (intentional). App store rejection. Payment processor account termination |
| **Must Contain** | Company name + contact info, types of data collected, purpose of collection, legal basis for processing, data retention periods, third-party services receiving data, user rights (access/delete/portability/correction), cookie disclosure, security measures, children's privacy (COPPA), cross-border transfer safeguards, "Do Not Sell/Share" link (CCPA), AI/LLM data usage disclosures |
| **Automated Checks** | Verify mentions of all data categories collected (scan code for data collection points), check for required CCPA "Do Not Sell" link, verify GDPR legal basis statements for each processing activity, check for cookie/tracking disclosure, verify contact information is present, check last-updated date < 12 months old |
| **Severity** | **CRITICAL** |

#### 1.2 Terms of Service (ToS) / Terms & Conditions

| Attribute | Detail |
|---|---|
| **Why Required** | Not strictly "legally required" but essential for enforceability. Required by app stores, payment processors, and SaaS platforms. Strongly recommended by every legal framework as it defines the contractual relationship |
| **Penalty if Missing** | Cannot enforce acceptable use, cannot limit liability, cannot enforce arbitration clauses, app store rejection, payment processor rejection. Without limitation of liability clause, unlimited damages exposure |
| **Must Contain** | Acceptance of terms, account registration, acceptable use policy, IP rights, user-generated content rights, payment terms + refund policy, service availability/uptime, limitation of liability, indemnification, termination conditions, dispute resolution (arbitration/courts), governing law, subscription terms (auto-renewal, billing cycle), API usage terms, data ownership/portability on termination, modification of terms notice period, DMCA compliance |
| **Automated Checks** | Verify presence of all required clauses (limitation of liability, indemnification, dispute resolution, governing law), check for auto-renewal disclosure compliance, verify DMCA agent registration, check that ToS references the privacy policy |
| **Severity** | **CRITICAL** |

#### 1.3 Cookie Policy / Cookie Consent Banner

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR (ePrivacy Directive), CCPA, multiple state laws. App stores require cookie disclosure. Payment processors require it |
| **Penalty if Missing** | GDPR fines up to €20M. CCPA enforcement actions. ePrivacy violations carry separate fines from data protection |
| **Must Contain** | Types of cookies (essential, analytics, marketing, functional), purpose of each category, duration (session vs persistent), third-party cookies (Google Analytics, Stripe, Intercom, etc.), how to manage/disable cookies, cookie consent mechanism (banner/popup), link to full privacy policy, GPC signal honoring |
| **Automated Checks** | Scan website for cookie consent banner presence, verify cookie categories are disclosed, check for "reject all" option (required in some jurisdictions), verify GPC/Do Not Track signal handling, check third-party cookie inventory completeness |
| **Severity** | **CRITICAL** |

#### 1.4 Terms of Service for App Stores (EULA / End User License Agreement)

| Attribute | Detail |
|---|---|
| **Why Required** | Required by Apple App Store and Google Play Store. Without it, your app cannot be listed |
| **Penalty if Missing** | App rejection/removal from stores |
| **Must Contain** | License grant, usage restrictions, IP ownership, warranty disclaimer, limitation of liability, termination, governing law |
| **Automated Checks** | Verify EULA is linked in app store listing, verify all required clauses present |
| **Severity** | **CRITICAL** |

---

### TIER 2: HIGH — Required for Specific Regulations or Lost Deals

#### 2.1 Data Processing Agreement (DPA) / Data Protection Addendum

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR (Art. 28) when you act as a data processor. Required by CCPA/CPRA service provider provisions. Required by TDPSA (Texas) with no revenue threshold. Required by all 20 US state privacy laws. Enterprise customers require this before signing |
| **Penalty if Missing** | GDPR: separate fines for processor violations. Enterprise deal failure. Customer lawsuits for non-compliance |
| **Must Contain** | Roles (controller/processor) per data category, processing purposes and instructions, subprocessor management (list + notification + objection right), data subject rights assistance, breach notification obligations, cross-border transfer safeguards (SCCs), data return/deletion on termination, audit rights, security measures |
| **Automated Checks** | Verify DPA exists and is referenced in ToS, check subprocessor list is current, verify breach notification timeline is specified (72hr GDPR), check for data return/deletion provisions, verify cross-border transfer mechanism documented |
| **Severity** | **HIGH** |

#### 2.2 Acceptable Use Policy (AUP)

| Attribute | Detail |
|---|---|
| **Why Required** | Enterprise customers require it. Required for SOC 2. Platform integrity. Protects against abuse liability |
| **Penalty if Missing** | Enterprise deal failure. Increased platform abuse. Potential liability for user abuse |
| **Must Contain** | Prohibited activities, content restrictions, security restrictions, API usage limits, spam/abuse policy, consequences of violation, reporting mechanism |
| **Automated Checks** | Verify AUP exists as separate document or section in ToS, check for specific prohibited activities list, verify enforcement mechanism described |
| **Severity** | **HIGH** |

#### 2.3 DMCA Policy / Copyright Policy

| Attribute | Detail |
|---|---|
| **Why Required** | Required by DMCA (Digital Millennium Copyright Act) for US-facing services. Safe harbor protection requires designated DMCA agent and takedown procedure |
| **Penalty if Missing** | Loss of DMCA safe harbor protection. Direct copyright infringement liability. Potential statutory damages |
| **Must Contain** | Designated DMCA agent contact, takedown procedure, counter-notification procedure, repeat infringer policy, good faith statement |
| **Automated Checks** | Verify DMCA agent is registered with US Copyright Office, check for takedown procedure description, verify repeat infringer policy exists |
| **Severity** | **HIGH** |

#### 2.4 GDPR-Specific Internal Documents

| Document | GDPR Article | Required When |
|---|---|---|
| Records of Processing Activities (ROPA) | Art. 30 | 250+ employees OR high-risk processing |
| Data Protection Impact Assessment (DPIA) | Art. 35 | High-risk processing (profiling, sensitive data, large-scale monitoring) |
| Data Breach Response Procedure | Art. 33-34 | Always (required to demonstrate readiness) |
| Data Breach Register | Art. 33 | Always |
| Data Retention Policy & Schedule | Art. 5, 13, 17, 30 | Always |
| Data Subject Consent Form | Art. 7 | When relying on consent as legal basis |
| Employee Privacy Notice | Art. 88 | When processing employee data in EU |
| Standard Contractual Clauses (SCCs) | Art. 46 | When transferring data outside EU/EEA |
| Data Protection Officer (DPO) Job Description | Art. 37-39 | When DPO appointment is mandatory |

| **Penalty if Missing** | GDPR fines up to €10M or 2% annual revenue for record-keeping violations |
| **Severity** | **HIGH** |

#### 2.5 CCPA/CPRA-Specific Requirements

| Requirement | Detail |
|---|---|
| "Do Not Sell or Share My Personal Information" Link | Must be prominently displayed on website |
| "Limit the Use of My Sensitive Personal Information" Link | Required by CPRA |
| Privacy Policy (CCPA-compliant) | Must list categories of PI collected, sources, purposes, third parties, retention periods |
| Consumer Request Mechanism | Must provide mechanism for access/deletion/correction requests |
| Annual Privacy Policy Update | Must be updated at least every 12 months |
| Data Protection Assessment | Required for high-risk processing (targeted ads, profiling, sensitive data) |
| Employee Training | Must train staff handling consumer data |
| Service Provider Agreements | Contracts with vendors must include CCPA compliance provisions |

| **Penalty if Missing** | $2,500/violation (negligent), $7,500/violation (intentional). Private right of action for data breaches |
| **Severity** | **HIGH** |

#### 2.6 Accessibility Statement / VPAT

| Attribute | Detail |
|---|---|
| **Why Required** | ADA Title III applies to websites/apps as "public accommodation." 5,000+ web accessibility lawsuits filed in 2025. EU European Accessibility Act (EAA) effective June 2025. Section 508 for federal contracts |
| **Penalty if Missing** | ADA lawsuits: $5K-$20K settlements typical. EAA: fines up to €30,000 + market bans. Section 508: contract loss |
| **Must Contain** | Commitment to accessibility, WCAG standard targeted (2.1 AA), known limitations, feedback mechanism, assessment methodology, date of assessment |
| **Automated Checks** | Automated WCAG scan (axe, Lighthouse), verify accessibility statement exists and is linked, check keyboard navigation, verify alt text presence, check color contrast ratios |
| **Severity** | **HIGH** |

---

### TIER 3: MEDIUM — Strongly Recommended (Bad Practice, Lost Deals)

#### 3.1 Refund / Cancellation Policy

| Attribute | Detail |
|---|---|
| **Why Required** | Required by payment processors (Stripe, Paddle). Reduces chargebacks. FTC auto-renewal rules apply. Some state laws require clear cancellation terms |
| **Penalty if Missing** | Payment processor account issues. Increased chargebacks. FTC enforcement under ROSCA. State AG actions |
| **Must Contain** | Refund window, refund process, cancellation process, subscription terms, auto-renewal disclosure, proration policy |
| **Automated Checks** | Verify refund policy exists and is linked from checkout/payment page, check for auto-renewal disclosure, verify cancellation process is described |
| **Severity** | **MEDIUM** |

#### 3.2 Security Policy / Information Security Policy

| Attribute | Detail |
|---|---|
| **Why Required** | Required for SOC 2 compliance. Required by GDPR (Art. 24, 32). Enterprise customers require it. Investor due diligence expects it |
| **Penalty if Missing** | SOC 2 audit failure. Enterprise deal failure. GDPR non-compliance. Increased breach liability |
| **Must Contain** | Security governance structure, access controls, encryption standards, incident response, vulnerability management, physical security, data classification, change management, business continuity |
| **Automated Checks** | Verify policy exists, check for annual review evidence, verify policy covers all SOC 2 Trust Services Criteria |
| **Severity** | **MEDIUM** |

#### 3.3 Incident Response / Breach Notification Policy

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR (Art. 33-34: 72-hour notification). Required by HIPAA (60-day notification). Required by CCPA. Required for SOC 2. Enterprise customers require documented plan |
| **Penalty if Missing** | GDPR: additional fines for delayed notification. HIPAA: penalties for late notification. SOC 2 audit findings. Enterprise deal failure |
| **Must Contain** | Detection procedures, classification/triage, containment steps, notification procedures (regulators + affected parties), evidence preservation, post-incident review, communication templates |
| **Automated Checks** | Verify policy exists with defined timelines, check that notification contacts are specified, verify escalation path documented |
| **Severity** | **MEDIUM** |

#### 3.4 Data Retention & Deletion Policy

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR (Art. 5(1)(e), Art. 17). Required by CCPA/CPRA. Required by COPPA. Part of SOC 2 data handling controls |
| **Penalty if Missing** | GDPR: data minimization violations. CCPA: inability to fulfill deletion requests. COPPA: retention violations |
| **Must Contain** | Retention periods per data category, automated deletion procedures, exceptions for legal holds, backup disposal procedures, data inventory |
| **Automated Checks** | Verify policy exists with specific timeframes (not vague language), check that automated deletion is described, verify alignment with privacy policy retention claims |
| **Severity** | **MEDIUM** |

#### 3.5 Employee Privacy Notice

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR (Art. 88) for EU employees. Best practice for all jurisdictions. Good faith requirement |
| **Penalty if Missing** | GDPR non-compliance. Employment disputes |
| **Must Contain** | What employee data is collected, purposes, legal basis, retention, rights, monitoring disclosure |
| **Automated Checks** | Verify notice exists and is provided to employees, check for required disclosures |
| **Severity** | **MEDIUM** |

#### 3.6 Subprocessor List

| Attribute | Detail |
|---|---|
| **Why Required** | Required by GDPR DPA obligations. Enterprise customers require transparency. SOC 2 vendor management |
| **Penalty if Missing** | DPA non-compliance. Enterprise deal delays. Customer objections |
| **Must Contain** | Current list of subprocessors, purpose of each, data location, notification mechanism for changes |
| **Automated Checks** | Verify list exists and is current, check that notification mechanism for changes is documented |
| **Severity** | **MEDIUM** |

#### 3.7 Vulnerability Disclosure / Bug Bounty Policy

| Attribute | Detail |
|---|---|
| **Why Required** | SOC 2 requirement. Enterprise customers expect responsible disclosure process. Industry best practice |
| **Penalty if Missing** | SOC 2 findings. Unreported vulnerabilities become unmanaged risks |
| **Must Contain** | Scope, submission process, safe harbor, response timeline, rewards (if any), legal protection |
| **Automated Checks** | Verify policy exists and is publicly accessible, check for safe harbor language |
| **Severity** | **MEDIUM** |

---

### TIER 4: CONDITIONAL — Required Only When Applicable

#### 4.1 HIPAA-Related Documents (Healthcare SaaS)

| Document | When Required |
|---|---|
| Business Associate Agreement (BAA) | When handling PHI for covered entities |
| HIPAA Security Risk Assessment | Always when handling PHI |
| HIPAA Privacy Policy | When handling PHI |
| Breach Notification Procedures (HIPAA-specific) | When handling PHI (60-day notification) |
| Workforce Training Documentation | When handling PHI |

**Penalty:** $100-$50,000/violation, up to $1.5M/year per violation category. Criminal penalties possible.
**Severity:** **CRITICAL** (if in healthcare vertical)

#### 4.2 COPPA Documents (Children Under 13)

| Document | When Required |
|---|---|
| COPPA-Compliant Privacy Policy | When directed to or knowingly collecting from children under 13 |
| Verifiable Parental Consent Mechanism | Before collecting children's personal information |
| Direct Notice to Parents | Before collecting children's data |
| Data Minimization Procedures | Always when handling children's data |

**Penalty:** $50,120/violation (2025 amount, adjusted annually). FTC enforcement.
**Severity:** **CRITICAL** (if serving children)

#### 4.3 SOC 2 Policy Suite

| Policy | SOC 2 TSC |
|---|---|
| Information Security Policy | Security (CC) |
| Access Control Policy | Security (CC) |
| Change Management Policy | Security (CC) |
| Incident Response Policy | Security (CC) |
| Risk Assessment Policy | Security (CC) |
| Data Classification Policy | Confidentiality |
| Acceptable Use Policy | Security (CC) |
| Vendor Management Policy | Security (CC) |
| Business Continuity/DR Policy | Availability |
| HR Security Policy | Security (CC) |
| Encryption Policy | Confidentiality |
| Backup & Recovery Policy | Availability |

**Penalty:** Not legally required, but enterprise sales blocker. Investors expect it for Series A+.
**Severity:** **HIGH** (for enterprise sales)

#### 4.4 ISO 27001 Documentation

| When Required | Enterprise customers (especially EU). Government contracts. Financial services |
|---|---|
| **Severity** | **MEDIUM-HIGH** (market-dependent) |

#### 4.5 Anti-Bribery / Anti-Corruption Policy

| When Required | International operations. Government contracts. Public companies |
|---|---|
| **Severity** | **MEDIUM** |

#### 4.6 Export Control / Sanctions Compliance

| When Required | International sales. Technology exports. US-origin software |
|---|---|
| **Severity** | **MEDIUM** |

#### 4.7 AI/ML-Specific Policies

| Document | When Required |
|---|---|
| AI Transparency Disclosure | When using AI in product (EU AI Act, Colorado AI Act, NYC Local Law 144) |
| AI Ethics Policy | Best practice for AI products |
| Automated Decision-Making Disclosure | GDPR Art. 22, CCPA profiling provisions |
| AI Training Data Disclosure | Colorado AI Act, EU AI Act |

**Penalty:** EU AI Act: up to €35M or 7% annual revenue for high-risk violations.
**Severity:** **HIGH** (if AI product)

---

## 2. Jurisdictional Requirements Map

### 2.1 Global / International

| Regulation | Scope | Key Requirements | Fine |
|---|---|---|---|
| **GDPR** (EU/EEA) | Any entity processing EU residents' data | Privacy notice, DPA, ROPA, DPIA, breach notification (72hr), DPO (if required), SCCs for international transfers, data subject rights | Up to €20M or 4% revenue |
| **EU AI Act** | AI systems in EU market | Risk classification, transparency, human oversight, data governance | Up to €35M or 7% revenue |
| **EU EAA** (European Accessibility Act) | Products/services in EU market | WCAG 2.1 AA / EN 301 549 conformance | Up to €30,000 + market ban |
| **UK GDPR** | UK residents' data | Same as GDPR (post-Brexit UK version) | Up to £17.5M or 4% revenue |
| **LGPD** (Brazil) | Brazilian residents' data | Similar to GDPR: privacy notice, DPO, consent, data subject rights | Up to 2% revenue, R$50M cap |
| **PIPEDA** (Canada) | Canadian residents' data | Privacy policy, consent, access rights, breach notification | Up to C$100K/violation |
| **PDPA** (Singapore) | Singapore residents' data | Consent, purpose limitation, access/correction | Up to S$1M |
| **APPI** (Japan) | Japanese residents' data | Privacy policy, consent for third-party transfers | Regulatory sanctions |

### 2.2 United States — Federal

| Law | Scope | Key Requirements | Penalty |
|---|---|---|---|
| **COPPA** | Children under 13 | Parental consent, privacy policy, data minimization, parental access/delete | $50,120/violation |
| **HIPAA** | Protected health information | BAA, Security Rule safeguards, Privacy Rule, breach notification (60 days) | $100-$50,000/violation, $1.5M/year |
| **FTC Act Section 5** | Unfair/deceptive practices | Honor privacy commitments, no deceptive claims | Varies |
| **CAN-SPAM** | Commercial email | Opt-out mechanism, physical address, no deceptive headers | $50,126/violation |
| **ADA Title III** | Public accommodation (websites/apps) | WCAG 2.1 AA accessibility | $5K-$20K settlements typical |
| **Section 508** | Federal government ICT | WCAG 2.0 A/AA (VPAT required for vendors) | Contract loss |
| **FCRA** | Consumer credit reports | Accuracy, dispute process, permissible purpose | $100-$1,000/violation |
| **GLBA** | Financial institutions | Privacy notice, safeguards, data sharing disclosures | Regulatory fines |

### 2.3 United States — State Privacy Laws (as of 2026)

| State | Law | Effective | Threshold | Key Distinction |
|---|---|---|---|---|
| California | CCPA/CPRA | Jan 2020/2023 | $25M revenue OR 100K consumers OR 50% data revenue | Broadest scope; private right of action for breaches; CPPA enforcement |
| Virginia | VCDPA | Jan 2023 | 100K consumers OR 25K + 50% data revenue | No private right of action; AG only |
| Colorado | CPA | Jul 2023 | 100K consumers OR 25K + 50% data revenue | Universal opt-out mechanism required |
| Connecticut | CTDPA | Jul 2023 | 100K consumers OR 25K + 25% data revenue | Profiling opt-out; covers loyalty programs |
| Utah | UCPA | Dec 2023 | $25M + 100K consumers OR 25K + 50% data revenue | Most business-friendly; high thresholds |
| Texas | TDPSA | Jul 2024 | **No revenue threshold** | Applies broadly to any entity doing business in TX |
| Oregon | OCPA | Jul 2024 | 100K consumers OR 25K + 25% data revenue | Covers nonprofits; employee data |
| Montana | MCDPA | Oct 2024 | **50K consumers** (lowest threshold) | Very low threshold |
| Iowa | ICDPA | Jan 2025 | 100K consumers OR 25K + 50% data revenue | 90-day cure period |
| Delaware | DPDPA | Jan 2025 | Low threshold tied to data volume | Very inclusive |
| New Hampshire | NHPA | Jan 2025 | Similar to CTDPA | Modeled after Connecticut |
| New Jersey | NJDPA | Jan 2025 | Broad "sale" definition | |
| Nebraska | NDPA | Jan 2025 | No revenue/consumer threshold | |
| Tennessee | TIPA | Jul 2025 | Standard | Affirmative defense for privacy programs |
| Minnesota | MPDPA | Jul 2025 | Standard | Profiling transparency |
| Maryland | MODPA | Oct 2025 | Standard | Strictest: data minimization by default, opt-in for sensitive data |
| Indiana | INCDPA | Jan 2026 | Standard | VCDPA-style |
| Kentucky | KCDPA | Jan 2026 | Standard | 60-day cure period |
| Rhode Island | RIDPA | Jan 2026 | Broad scope | Includes small businesses |

### 2.4 Other State-Specific Requirements

| Law | State | Requirement |
|---|---|---|
| **NY SHIELD Act** | New York | Data security program required, breach notification within "most expedient time" |
| **Illinois BIPA** | Illinois | Written consent for biometric data; $1,000-$5,000/violation |
| **Washington MHMD Act** | Washington | Consumer health data protections; opt-in consent |
| **CIPA** | Various | Children's Internet Protection Act (affects schools/libraries) |

---

## 3. Investor & Enterprise Customer Requirements

### 3.1 What Investors Require (Due Diligence)

| Document/Requirement | Stage | Why |
|---|---|---|
| **Incorporation documents + bylaws** | All | Corporate hygiene |
| **Cap table** | All | Ownership verification |
| **Privacy Policy** | Pre-seed+ | Legal compliance verification |
| **Terms of Service** | Pre-seed+ | Contractual framework |
| **IP assignment agreements** | Seed+ | IP ownership proof |
| **DPA** | Seed+ | GDPR/CCPA compliance |
| **SOC 2 Type II report** | Series A+ | Security posture validation |
| **Penetration test report** | Series A+ | Security validation |
| **Data breach history** | All | Risk assessment |
| **Employee handbook + policies** | Seed+ | Operational maturity |
| **Customer contracts** | Seed+ | Revenue validation |
| **NDA/compliance framework** | Seed+ | Information protection |
| **Regulatory compliance documentation** | Series A+ | Sector-specific compliance |

### 3.2 What Enterprise Customers Require (Security Questionnaires)

Enterprise sales typically require passing a vendor security assessment. The most common frameworks:

| Framework | Questions | When Required |
|---|---|---|
| **SIG (Standardized Information Gathering)** | 100-800 questions | Large enterprise, financial services |
| **CAIQ (Cloud Assurance Questionnaire)** | 300+ questions | Cloud/SaaS vendors |
| **HRCI/HECVAT** | 100+ questions | Higher education, healthcare |
| **Custom questionnaires** | Varies | Most enterprise sales |

**Typical enterprise checklist items:**
- SOC 2 Type II report (or willingness to obtain)
- Penetration test results (executive summary)
- Signed DPA/Data Processing Addendum
- Privacy Policy + Terms of Service
- Information Security Policy
- Incident Response Plan
- Business Continuity/DR Plan
- Vulnerability Management Program
- Access Control Policy
- Encryption standards documentation (AES-256, TLS 1.2+)
- Data residency information
- Subprocessor list
- BAAs (if healthcare)
- Insurance certificates (Cyber, E&O)
- Evidence of annual security training
- Evidence of background checks
- Evidence of access reviews
- Evidence of vulnerability scanning/patching
- Disaster recovery test results
- Evidence of data classification

---

## 4. Minimum Viable Policy Set for Startups

### Phase 1: Pre-Launch / Pre-Revenue (Day 1)

| # | Policy | Priority | Est. Cost |
|---|---|---|---|
| 1 | **Privacy Policy** | CRITICAL | $0-$500 (template) or $1,500-$5,000 (attorney) |
| 2 | **Terms of Service** | CRITICAL | $0-$500 (template) or $2,000-$8,000 (attorney) |
| 3 | **Cookie Policy + Consent Banner** | CRITICAL | $0-$100/mo (Termly/CookieScript) |
| 4 | **Refund/Cancellation Policy** | MEDIUM | Included in ToS or $0-$200 |
| 5 | **DMCA Policy** | HIGH | $0 (template) + US Copyright Office agent registration ($6) |

**Total Phase 1 cost:** $0-$13,700 depending on DIY vs attorney

### Phase 2: First Revenue / First Enterprise Customer

| # | Policy | Priority | Est. Cost |
|---|---|---|---|
| 6 | **Data Processing Agreement (DPA)** | HIGH | $500-$3,000 (attorney) |
| 7 | **Acceptable Use Policy** | HIGH | $0-$500 |
| 8 | **Security Policy** | MEDIUM | $0-$1,000 |
| 9 | **Subprocessor List** | MEDIUM | $0 (internal doc) |
| 10 | **Data Retention Policy** | MEDIUM | $0-$500 |

**Total Phase 2 cost:** $500-$5,000

### Phase 3: Scaling / SOC 2 Pursuit / Series A

| # | Policy | Priority | Est. Cost |
|---|---|---|---|
| 11 | **Incident Response Plan** | MEDIUM | $1,000-$5,000 |
| 12 | **Access Control Policy** | HIGH (SOC 2) | $500-$2,000 |
| 13 | **Change Management Policy** | HIGH (SOC 2) | $500-$2,000 |
| 14 | **Business Continuity/DR Policy** | HIGH (SOC 2) | $1,000-$3,000 |
| 15 | **Vendor Management Policy** | HIGH (SOC 2) | $500-$2,000 |
| 16 | **Data Classification Policy** | MEDIUM | $500-$1,500 |
| 17 | **HR Security Policy** | MEDIUM | $500-$1,500 |
| 18 | **Acceptable Use Policy (Employee)** | MEDIUM | $0-$500 |
| 19 | **Employee Privacy Notice** | MEDIUM | $500-$1,500 |
| 20 | **Vulnerability Disclosure Policy** | MEDIUM | $0-$500 |
| 21 | **Accessibility Statement** | MEDIUM | $500-$2,000 |
| 22 | **AI Ethics/Transparency Policy** | MEDIUM | $1,000-$5,000 |

**Total Phase 3 cost:** $6,000-$27,000

### Phase 4: Enterprise-Ready / International

| # | Policy | Priority | Est. Cost |
|---|---|---|---|
| 23 | **ROPA (Records of Processing Activities)** | HIGH (GDPR) | $2,000-$10,000 |
| 24 | **DPIA Template** | HIGH (GDPR) | $1,000-$5,000 |
| 25 | **Standard Contractual Clauses (SCCs)** | HIGH (GDPR) | $2,000-$10,000 |
| 26 | **BAA (HIPAA)** | CRITICAL (healthcare) | $2,000-$8,000 |
| 27 | **SOC 2 Policy Suite** | HIGH | $5,000-$25,000 (with compliance platform) |
| 28 | **ISO 27001 Documentation** | MEDIUM | $10,000-$50,000 |

---

## 5. Automated Compliance Checks

### 5.1 Privacy Policy Automated Checks

| Check | What to Verify | Method |
|---|---|---|
| **Data category completeness** | Privacy policy mentions all data types collected by the app | Cross-reference data collection points in code with policy disclosures |
| **Third-party disclosure** | All third-party services (analytics, payment, etc.) are listed | Scan code for third-party SDKs/APIs and verify each is mentioned |
| **Legal basis statements** | GDPR legal basis provided for each processing activity | NLP check for legal basis keywords per data category |
| **CCPA "Do Not Sell" link** | Link exists and is functional | Automated link checker |
| **Right to delete mechanism** | Process for data deletion requests is described | Check for deletion request instructions |
| **Retention periods** | Specific retention timeframes (not vague "as needed") | Regex check for time period statements |
| **Freshness** | Updated within last 12 months | Parse "Last Updated" date |
| **Contact information** | DPO/contact email is present | Regex for email pattern |
| **Cross-border transfers** | International data transfers are disclosed | Check for country/region mentions |
| **Cookie disclosure** | Cookies/tracking technologies are mentioned | Keyword scan |

### 5.2 Terms of Service Automated Checks

| Check | What to Verify | Method |
|---|---|---|
| **Limitation of liability** | Clause exists with specific cap | NLP check for liability limitation language |
| **Indemnification** | Mutual indemnification clause present | Check for indemnification section |
| **Dispute resolution** | Arbitration or jurisdiction specified | Check for arbitration/governing law clause |
| **Governing law** | Jurisdiction is specified | Regex for state/country name |
| **Termination provisions** | Conditions for termination described | Check for termination section |
| **Auto-renewal disclosure** | Subscription auto-renewal terms disclosed | Check for auto-renewal language |
| **DMCA reference** | DMCA policy is referenced or included | Check for DMCA mention |
| **Privacy Policy cross-reference** | Links to privacy policy | Check for privacy policy link |
| **Modifications clause** | Process for changing terms is described | Check for modification notice requirements |

### 5.3 Cookie Policy Automated Checks

| Check | What to Verify | Method |
|---|---|---|
| **Consent banner present** | Cookie consent mechanism is active | DOM inspection for consent banner |
| **Reject option available** | "Reject all" option exists | UI check for reject button |
| **Cookie categories disclosed** | Essential, analytics, marketing, functional categories | Text content check |
| **GPC signal honoring** | Global Privacy Control signal is respected | Browser automation test |
| **Third-party cookies listed** | All third-party cookies identified | Cookie inventory comparison |

### 5.4 Code-Level Compliance Checks

| Check | What to Verify | Method |
|---|---|---|
| **Consent-gated tracking** | Analytics/tracking only fires after consent | Network request monitoring pre/post consent |
| **Data collection points** | All PII collection is documented | Static analysis for data collection patterns |
| **Encryption in transit** | TLS 1.2+ enforced on all endpoints | SSL/TLS configuration scan |
| **Encryption at rest** | Sensitive data encrypted in storage | Configuration audit |
| **No secrets in code** | API keys, secrets not hardcoded | Secret scanning (truffleHog, gitleaks) |
| **No PII in logs** | Personal data not logged | Log content scanning |
| **Access control** | Role-based access control implemented | Code review for auth patterns |
| **Audit logging** | Security events are logged | Verify logging implementation |

### 5.5 Infrastructure Compliance Checks

| Check | What to Verify | Method |
|---|---|---|
| **SSL certificate valid** | TLS certificate is current and valid | SSL certificate scanner |
| **Security headers** | CSP, HSTS, X-Frame-Options, etc. present | HTTP header scanner |
| **CORS configuration** | Not overly permissive | CORS configuration check |
| **Dependency vulnerabilities** | No known CVEs in dependencies | `npm audit`, `pip audit`, Snyk scan |
| **Open ports** | No unnecessary open ports | Port scan |
| **Database permissions** | Minimal required permissions | Database configuration audit |
| **Backup configuration** | Backups are configured and encrypted | Infrastructure audit |

---

## 6. Consequences of Non-Compliance

### 6.1 By Regulation

| Regulation | Maximum Fine | Notable Enforcement |
|---|---|---|
| **GDPR** | €20M or 4% annual revenue | Meta: €1.2B (2023). Amazon: €746M (2021). TikTok: €345M (2023) |
| **CCPA/CPRA** | $2,500-$7,500/violation | Sephora: $1.2M (2022). Tilting Point/TerraCore: first private action |
| **COPPA** | $50,120/violation (2025) | Epic Games: $275M (2022). Microsoft: $20M (2023) |
| **HIPAA** | $1.5M/year/violation category | Anthem: $16M (2020). Premera: $6.85M (2020) |
| **ADA Title III** | $5K-$20K settlement typical | 5,000+ web lawsuits in 2025 alone |
| **FTC Act** | Varies per case | Epic Games: $245M (2022) |
| **State privacy laws** | Varies ($2,500-$7,500/violation typical) | Texas AG actions increasing 2025-2026 |
| **EU AI Act** | €35M or 7% annual revenue | Enforceable from August 2025 |

### 6.2 By Business Impact

| Missing Policy | Business Consequence |
|---|---|
| No Privacy Policy | App store rejection, payment processor termination, regulatory fines, cannot sell to enterprises |
| No ToS | Cannot enforce terms, unlimited liability exposure, payment processor rejection |
| No DPA | Cannot process EU customer data, enterprise deal failure |
| No SOC 2 | Cannot sell to enterprises (50%+ of B2B deals require it) |
| No BAA | Cannot serve healthcare customers |
| No Accessibility Statement | ADA lawsuit exposure, government contract exclusion |
| No Cookie Consent | GDPR/ePrivacy fines, EU market access blocked |
| No DMCA Policy | Loss of safe harbor, copyright infringement liability |
| No Incident Response Plan | Delayed breach response, increased regulatory penalties |
| No Security Policy | SOC 2 failure, enterprise deal failure, investor red flag |

### 6.3 By Deal Impact

| Scenario | Revenue at Risk |
|---|---|
| Enterprise customer asks for SOC 2 and you don't have it | $50K-$500K+ annual deal lost |
| Enterprise asks for signed DPA and you can't provide one | $100K-$1M+ deal stalled for months |
| Security questionnaire comes back with "N/A" for most questions | Deal likely lost or pushed to next quarter |
| Investor due diligence finds missing IP assignments | Valuation reduction or deal collapse |
| Customer data breach without incident response plan | Regulatory fine + customer churn + reputation damage |

---

## Appendix A: Policy Document Template Checklist

For each policy document, verify:

- [ ] Document has a unique identifier/version number
- [ ] Document has an approval date and approver name
- [ ] Document has a "last reviewed" date (reviewed within last 12 months)
- [ ] Document is accessible to all affected parties
- [ ] Document has an attestation/acknowledgment mechanism
- [ ] Document maps to applicable regulatory requirements
- [ ] Document has supporting procedures
- [ ] Evidence of enforcement is collected and stored

## Appendix B: Recommended Tools

| Category | Tools |
|---|---|
| **Policy Generation** | Termly, PrivacyPolicies.com, Iubenda |
| **Consent Management** | CookieScript, OneTrust, Cookiebot, Usercentrics |
| **Compliance Automation** | Vanta, Drata, SecureSlate, Sprinto |
| **Security Scanning** | Snyk, TruffleHog, npm audit, OWASP ZAP |
| **Accessibility** | axe, Lighthouse, WAVE, AudioEye |
| **SOC 2 Readiness** | Vanta, Drata, Laika, Tugboat Logic |
| **Legal Review** | Promise Legal, LegalZoom, Clerky (for incorporation) |

---

*This research is for informational purposes and does not constitute legal advice. Consult qualified legal counsel for compliance decisions specific to your business.*
