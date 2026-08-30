# Compliance, Policies, and Legal Documents

**Category ID:** `compliance`

---

## Scope

Inspect all legal policies, compliance documents, regulatory requirements, and business disclosures. Missing policies cause lawsuits, regulatory fines, lost enterprise deals, and app store removal. This category checks whether your project has the documents it needs and whether those documents are actually complete.

---

## Checks

### Privacy Policy
- Missing privacy policy
- Privacy policy not linked from website/app
- Privacy policy not linked from mobile app stores (Apple, Google)
- Privacy policy does not disclose what data is collected
- Privacy policy does not disclose how data is used
- Privacy policy does not disclose data sharing practices
- Privacy policy does not disclose data retention periods
- Privacy policy does not disclose user rights (access, deletion, correction)
- Privacy policy does not disclose contact information for privacy inquiries
- Privacy policy does not disclose cookie usage
- Privacy policy does not disclose third-party services used
- Privacy policy does not disclose international data transfers
- Privacy policy does not disclose legal basis for processing (GDPR)
- Privacy policy does not disclose data controller identity
- Privacy policy does not disclose data protection officer contact
- Privacy policy does not disclose children's data handling (COPPA)
- Privacy policy does not disclose AI/ML data usage
- Privacy policy does not disclose user data deletion process
- Privacy policy not updated in last 12 months
- Privacy policy references wrong company name or domain
- Privacy policy contradicts actual data practices in code
- Privacy policy does not list all 20 US state privacy law rights (CA, VA, CO, CT, UT, IA, IN, KY, TN, TX, FL, OR, MT, NJ, NH, DE, MD, NE, MN, RI)
- Privacy policy missing Texas TDPSA disclosure (no revenue threshold)
- Privacy policy missing Maryland MODPA disclosure (strictest: data minimization, opt-in for sensitive data)

### Terms of Service
- Missing terms of service
- Terms of service not linked from website/app
- Terms of service does not define acceptable use
- Terms of service does not define prohibited conduct
- Terms of service does not limit liability
- Terms of service does not define governing law
- Terms of service does not define dispute resolution mechanism
- Terms of service does not define termination conditions
- Terms of service does not define user content ownership
- Terms of service does not define service availability
- Terms of service does not define modification terms
- Terms of service does not define indemnification
- Terms of service does not address DMCA/copyright policy
- Terms of service references wrong company name or domain
- Terms of service not updated in last 12 months

### Cookie Policy and Consent
- Missing cookie policy
- Cookie policy does not list all cookies used
- Cookie policy does not disclose cookie purposes
- Cookie policy does not disclose cookie duration
- Cookie policy does not disclose third-party cookies
- Missing cookie consent banner/mechanism
- Cookie consent does not allow granular control
- Cookie consent does not allow rejection of non-essential cookies
- Cookie consent does not remember user preference
- Missing opt-out mechanism for sale of personal information (CCPA)
- Missing "Do Not Sell or Share My Personal Information" link (CCPA)
- Missing "Limit the Use of My Sensitive Personal Information" link (CCPA)
- Cookie consent not implemented before cookies are set (GDPR)
- Missing ePrivacy compliance for electronic communications

### End User License Agreement (EULA)
- Missing EULA for mobile/desktop applications
- EULA not linked in app store listing
- EULA does not define license grant
- EULA does not define restrictions
- EULA does not define ownership
- EULA does not address third-party components
- EULA does not address export compliance

### Data Processing Agreement (DPA)
- Missing DPA for GDPR compliance
- DPA does not define processing purposes
- DPA does not define data categories
- DPA does not define data subject categories
- DPA does not define sub-processor list
- DPA does not define data transfer mechanisms
- DPA does not define security measures
- DPA does not define breach notification obligations
- DPA does not define data return/deletion obligations
- Missing standard contractual clauses (SCCs) for international transfers
- Missing DPA template for customers to sign

### DMCA / Copyright Policy
- Missing DMCA policy
- DMCA policy does not define designated agent
- DMCA policy does not define takedown procedure
- DMCA policy does not define counter-notification procedure
- DMCA policy does not address repeat infringers
- Missing DMCA agent registration with US Copyright Office
- Missing safe harbor protections due to missing DMCA policy

### Acceptable Use Policy (AUP)
- Missing AUP
- AUP does not prohibit illegal activity
- AUP does not prohibit abuse/harassment
- AUP does not prohibit spam
- AUP does not prohibit malware distribution
- AUP does not prohibit unauthorized access attempts
- AUP does not define enforcement actions

### Security Policy / Statement
- Missing security policy or trust page
- Security policy does not describe encryption practices
- Security policy does not describe access controls
- Security policy does not describe incident response
- Security policy does not describe vulnerability disclosure
- Security policy does not describe penetration testing
- Security policy does not describe data backups
- Security policy does not describe availability/uptime commitments
- Missing security contact or responsible disclosure channel
- Missing bug bounty program or vulnerability reporting process

### Refund Policy
- Missing refund policy
- Refund policy does not define refund conditions
- Refund policy does not define refund timeline
- Refund policy does not define partial refund terms
- Refund policy does not address subscription cancellations
- Refund policy contradicts payment processor requirements

### Service Level Agreement (SLA)
- Missing SLA for enterprise customers
- SLA does not define uptime guarantee
- SLA does not define support response times
- SLA does not define escalation procedures
- SLA does not define service credits for missed SLAs

### Accessibility Statement
- Missing accessibility statement
- Accessibility statement does not define conformance level (WCAG 2.1 AA)
- Accessibility statement does not describe known limitations
- Accessibility statement does not provide feedback mechanism
- Accessibility statement does not define testing methodology
- Missing VPAT (Voluntary Product Accessibility Template) for enterprise sales
- Missing ADA compliance documentation
- Missing European Accessibility Act (EAA) compliance

### AI-Specific Disclosures
- Missing AI transparency disclosure
- Missing disclosure that AI is used in the product
- Missing disclosure of AI limitations
- Missing disclosure of AI bias risks
- Missing disclosure of human oversight availability
- Missing AI content labeling for generated content
- Missing disclosure of training data sources
- Missing opt-out of AI training on user data

### Regulatory Compliance (Conditional)
- Missing HIPAA compliance documentation (if healthcare)
- Missing BAA (Business Associate Agreement) template (if healthcare)
- Missing SOC 2 Type I/II report (if enterprise SaaS)
- Missing ISO 27001 certification (if enterprise)
- Missing PCI DSS compliance (if processing payments)
- Missing COPPA compliance (if children under 13)
- Missing FERPA compliance (if education)
- Missing FedRAMP authorization (if government)

### SOC 2 Policy Suite (Conditional)
- Missing information security policy
- Missing access control policy
- Missing change management policy
- Missing incident response policy
- Missing risk management policy
- Missing vendor management policy
- Missing data classification policy
- Missing data retention policy
- Missing business continuity policy
- Missing disaster recovery policy
- Missing acceptable use policy
- Missing security awareness training policy

---

## Methodology

1. Search for all policy files in the repository (privacy, terms, cookies, DMCA, etc.)
2. Check that policies are linked from the website, app, and app store listings
3. Verify each policy contains all required clauses
4. Check policy currency (updated within last 12 months)
5. Cross-reference policy statements against actual code behavior
6. Verify consent mechanisms are implemented correctly
7. Check for regulatory requirements based on business model and geography
8. Verify enterprise compliance documents exist (SOC 2, DPA, SLA)
9. Check AI-specific disclosures if AI is used
10. Verify accessibility compliance documentation

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| No privacy policy | CRITICAL |
| No terms of service | CRITICAL |
| Privacy policy contradicts actual data practices | CRITICAL |
| Missing cookie consent (GDPR) | CRITICAL |
| Missing DMCA policy (no safe harbor) | HIGH |
| Missing DPA (GDPR Art. 28) | HIGH |
| Missing accessibility statement (ADA/EAA) | HIGH |
| Missing refund policy | MEDIUM |
| Missing security/trust page | MEDIUM |
| Missing AI transparency disclosure | MEDIUM |
| Outdated policies (>12 months) | LOW |
| Missing SLA for enterprise | MEDIUM |

---

## Evidence Requirements

- Which policies exist and which are missing
- Which required clauses are absent from existing policies
- Whether policies are linked from the product
- Whether policies match actual data practices
- Which regulations apply based on business model and geography
- Whether consent mechanisms are properly implemented
