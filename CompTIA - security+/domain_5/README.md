# Domain 5.0: Security Program Management and Oversight
**CompTIA Security+ SY0-701 | Exam Weight: ~20%**

Covers the governance, compliance, risk management, and audit frameworks that underpin a mature security program. Also includes third-party risk and building a security-aware culture. Expect policy-heavy scenario questions.

---

## Table of Contents
- [Acronyms Quick Reference](#acronyms-quick-reference)
- [5.1 Security Governance](#51-security-governance)
- [5.2 Risk Management Process](#52-risk-management-process)
- [5.3 Third-Party Risk Management](#53-third-party-risk-management)
- [5.4 Security Compliance](#54-security-compliance)
- [5.5 Audits and Assessments](#55-audits-and-assessments)
- [5.6 Security Awareness Practices](#56-security-awareness-practices)
- [Study Checklist](#study-checklist)

---

## Acronyms Quick Reference

| Acronym | Full Term | Quick Context |
|---------|-----------|---------------|
| **AUP** | Acceptable Use Policy | Rules governing how employees may use organizational IT resources |
| **BIA** | Business Impact Analysis | Identifies critical functions and the consequences of their disruption |
| **MTBF** | Mean Time Between Failures | Average operational time before a system failure |
| **MTTR** | Mean Time to Repair | Average time to restore a failed system |
| **RTO** | Recovery Time Objective | Maximum acceptable downtime after a disruption |
| **RPO** | Recovery Point Objective | Maximum acceptable data loss measured in time |
| **SLA** | Service Level Agreement | Contractual commitment defining the level of service a provider must deliver |
| **MOU** | Memorandum of Understanding | Non-binding agreement outlining shared goals between parties |
| **MSA** | Master Service Agreement | Overarching contract governing the general terms of a vendor relationship |
| **SOW** | Statement of Work | Document specifying the work to be performed, deliverables, and timeline |
| **NDA** | Non-Disclosure Agreement | Legally binding contract prohibiting disclosure of confidential information |
| **GDPR** | General Data Protection Regulation | EU regulation governing data privacy and protection rights |
| **PCI DSS** | Payment Card Industry Data Security Standard | Security standard for organizations handling branded payment card data |
| **HIPAA** | Health Insurance Portability and Accountability Act | US law protecting the privacy and security of medical information |
| **ISO** | International Organization for Standardization | International body publishing security standards (e.g., ISO/IEC 27001) |
| **NIST** | National Institute of Standards and Technology | US federal agency publishing security frameworks (NIST CSF, NIST SP 800 series) |
| **SOC 2** | Service Organization Control 2 | Audit report verifying a service provider's security, availability, and privacy controls |
| **CSA** | Cloud Security Alliance | Industry body publishing cloud security standards (e.g., CCM, STAR) |

---

## 5.1 Security Governance
*Summarize elements of effective security governance.*

### Governance Framework

Security governance is the set of rules, responsibilities, and practices by which an organization directs and controls its security program. It ensures security initiatives align with business objectives and risk appetite.

### Policy Hierarchy

| Document Type | Scope | Examples |
|---------------|-------|---------|
| **Policy** | High-level statement of management intent and direction | Information Security Policy, AUP, Data Classification Policy |
| **Standard** | Specific, mandatory requirements that support a policy | Password complexity standard: min 12 characters, 1 uppercase, 1 number |
| **Procedure** | Step-by-step instructions for implementing a policy or standard | Account provisioning procedure, incident escalation procedure |
| **Guideline** | Recommended but not mandatory best practices | Recommendations for securing home office workstations |

> **Exam Tip:** Policies are **mandatory** (what must be done). Standards are **mandatory** (specific requirements). Procedures are **mandatory** (how to do it). Guidelines are **recommended** but not enforced. Standards and procedures flesh out the intent of policies.

### Key Security Policies

| Policy | Purpose |
|--------|---------|
| **Acceptable Use Policy (AUP)** | Defines permitted and prohibited use of organizational IT resources |
| **Data Classification Policy** | Defines sensitivity tiers and handling requirements for data |
| **Password / Authentication Policy** | Specifies complexity, length, expiry, and MFA requirements |
| **Change Management Policy** | Governs how changes are requested, reviewed, approved, and documented |
| **Incident Response Policy** | Defines roles, responsibilities, and procedures for handling security incidents |
| **Business Continuity Policy** | Establishes requirements for maintaining critical operations during disruptions |

### Governance Roles

| Role | Responsibility |
|------|---------------|
| **Board / Executive** | Set risk appetite; approve security budget and strategy |
| **CISO** | Own the security program; report to executive leadership |
| **Data Owner** | Business owner responsible for a data set's classification and protection |
| **Data Custodian** | IT team member responsible for implementing controls specified by the data owner |
| **Data Steward** | Ensures data quality and governance compliance |
| **End User** | Responsible for following policies and reporting suspected incidents |

---

## 5.2 Risk Management Process
*Explain elements of the risk management process.*

### Risk Management Lifecycle

```
Identify Risks → Assess (Likelihood × Impact) → Prioritize → Select Response → Implement Controls → Monitor → Repeat
```

### Risk Terminology

| Term | Definition |
|------|------------|
| **Threat** | A potential cause of harm (e.g., ransomware, hurricane, insider) |
| **Vulnerability** | A weakness that a threat can exploit (e.g., unpatched software) |
| **Risk** | The potential for harm = Threat × Vulnerability × Impact |
| **Likelihood** | Probability that a threat will exploit a vulnerability |
| **Impact** | Magnitude of harm if the risk materializes |
| **Risk Appetite** | The level of risk the organization is willing to accept in pursuit of its objectives |
| **Residual Risk** | Risk that remains after controls have been implemented |
| **Inherent Risk** | Risk that exists before any controls are applied |

### Risk Response Strategies

| Strategy | Description | Example |
|----------|-------------|---------|
| **Mitigation (Reduction)** | Implement controls to reduce likelihood or impact | Patch a vulnerability; deploy a firewall |
| **Transfer** | Shift the financial impact of risk to a third party | Purchase cyber liability insurance; outsource to an MSSP |
| **Acceptance** | Acknowledge the risk and take no action; typically documented formally | Accept a low-severity risk that is too costly to mitigate |
| **Avoidance** | Eliminate the risk by not engaging in the risky activity | Discontinue a high-risk service or feature |

> **Exam Tip:** **Risk transfer** does not eliminate the risk — it transfers the **financial consequences**. The organization still bears reputational and operational risks. Insurance is the primary example; contractual clauses shifting liability to a vendor are another.

### Quantitative vs. Qualitative Risk Analysis

| Type | Approach | Output |
|------|----------|--------|
| **Quantitative** | Assigns numerical values to likelihood and impact | ALE (Annual Loss Expectancy) = ARO × SLE |
| **Qualitative** | Uses descriptive categories (High/Medium/Low) | Risk matrix / heat map |

**Key quantitative risk formulas:**
- **SLE** (Single Loss Expectancy) = Asset Value × Exposure Factor
- **ARO** (Annualized Rate of Occurrence) = Expected frequency of the threat per year
- **ALE** (Annualized Loss Expectancy) = SLE × ARO

---

## 5.3 Third-Party Risk Management
*Explain the processes associated with third-party risk assessment and management.*

### Why Third-Party Risk Matters
Third-party vendors, contractors, and partners who have access to your systems, data, or supply chain represent a significant attack surface. Breaches through trusted third parties are common and high-impact (e.g., Target breach via HVAC contractor, SolarWinds supply chain attack).

### Vendor Assessment Process

| Step | Activities |
|------|-----------|
| **Due Diligence** | Review vendor security policies, certifications (SOC 2, ISO 27001), breach history, and references |
| **Risk Assessment** | Evaluate the sensitivity of data shared and the access level granted |
| **Questionnaires** | Use standardized assessments (CSA CAIQ, SIG Lite) to gather vendor security details |
| **Penetration testing / audit** | For high-risk vendors, require independent security assessments |
| **Continuous Monitoring** | Ongoing monitoring of vendor security posture via threat intelligence and re-assessments |

### Third-Party Agreements

| Agreement | Binding | Purpose |
|-----------|---------|---------|
| **NDA** (Non-Disclosure Agreement) | Yes — legal contract | Prohibits disclosure of confidential information shared during the engagement |
| **MOU** (Memorandum of Understanding) | No — non-binding | Outlines shared goals and intentions between parties; precedes formal contracts |
| **MSA** (Master Service Agreement) | Yes | Establishes overarching terms governing all future transactions between two parties |
| **SOW** (Statement of Work) | Yes | Specifies deliverables, timeline, milestones, and acceptance criteria for a specific project |
| **SLA** (Service Level Agreement) | Yes | Defines minimum acceptable service levels (uptime, response times, support tiers) |
| **BPA** (Business Partnership Agreement) | Yes | Governs terms of a broader business relationship or partnership |

> **Exam Tip:** Know what each agreement is designed to protect. **NDA** → confidentiality of shared information. **SLA** → service performance guarantees. **MOU** → non-binding intent. **MSA** → overarching contract terms. **SOW** → specific project scope and deliverables.

### Rules of Engagement and Right to Audit
Contracts with high-risk vendors should include:
- **Right-to-audit clauses** — the right to assess the vendor's security controls
- **Data handling requirements** — specifying how data must be stored, transmitted, and destroyed
- **Breach notification obligations** — vendor must notify within a defined timeframe (e.g., 24–72 hours)
- **Termination and data return/destruction clauses**

---

## 5.4 Security Compliance
*Summarize elements of effective security compliance.*

### Types of Compliance Obligations

| Type | Source | Examples |
|------|--------|---------|
| **Regulatory** | Government law or regulation | GDPR (EU), HIPAA (US healthcare), SOX (financial reporting), FERPA (education) |
| **Industry / Contractual** | Industry standards required by contract | PCI DSS (payment card processing) |
| **Internal** | Organizational self-imposed policy | ISO/IEC 27001, NIST CSF adoption |

### Key Compliance Frameworks

| Framework | Scope | Key Focus |
|-----------|-------|----------|
| **GDPR** | EU citizens' personal data | Privacy rights, consent, data minimization, 72-hour breach notification |
| **HIPAA** | US healthcare (PHI) | Privacy Rule, Security Rule, Breach Notification Rule |
| **PCI DSS** | Payment card data | 12 requirements; tokenization, encryption, access control, logging |
| **SOX** | US public companies | Financial data integrity; IT controls over financial systems |
| **NIST CSF** | Any organization | Framework: Identify, Protect, Detect, Respond, Recover |
| **ISO/IEC 27001** | Any organization | Information Security Management System (ISMS) certification |
| **SOC 2** | Service providers | Trust Services Criteria: Security, Availability, Confidentiality, Processing Integrity, Privacy |

### Privacy Concepts

| Concept | Definition |
|---------|-----------|
| **PII** (Personally Identifiable Information) | Data that can identify a specific individual (name, SSN, email, IP address) |
| **PHI** (Protected Health Information) | Medical information tied to an individual; governed by HIPAA |
| **Data Subject** | Individual whose personal data is being processed |
| **Data Processor** | Entity that processes data on behalf of the data controller |
| **Data Controller** | Entity that determines the purposes and means of processing personal data |
| **Right to be Forgotten** | GDPR right allowing individuals to request deletion of their personal data |

---

## 5.5 Audits and Assessments
*Explain types and purposes of audits and assessments.*

### Audit Types

| Type | Performed By | Objectivity | Use Case |
|------|-------------|-------------|---------|
| **Internal Audit** | Organization's own audit team | Less independent | Ongoing compliance verification; pre-external audit preparation |
| **External Audit** | Independent third-party firm | Fully independent | Regulatory compliance; customer assurance; attestation reports |
| **Certification Audit** | Accredited certification body | Fully independent | Obtaining ISO 27001, SOC 2 certifications |

### Assessment Types

| Assessment | Description | Output |
|------------|-------------|--------|
| **Vulnerability Assessment** | Automated scanning to identify known vulnerabilities; does not exploit them | Prioritized list of vulnerabilities |
| **Penetration Test** | Simulated attack that actively exploits vulnerabilities to demonstrate impact | Proof-of-concept exploits, detailed remediation recommendations |
| **Red Team Exercise** | Full-scope attack simulation mimicking a real adversary over an extended period | TTPs used, detection gaps identified |
| **Blue Team / Purple Team** | Defenders (Blue); collaborative offense-defense exercise (Purple) | Improved detection rules, response validation |
| **Risk Assessment** | Evaluates likelihood and impact of identified threats | Risk register with prioritized risks |
| **Threat Modeling** | Systematic identification of threats against a specific application or system | STRIDE/DREAD analysis, threat mitigations |

> **Exam Tip — Vulnerability Assessment vs. Penetration Test:**
> - **Vulnerability assessment** = *finds* weaknesses (scanning, non-exploiting)
> - **Penetration test** = *proves* impact by actively exploiting weaknesses
> A pentest always begins with a scope agreement and rules of engagement. Unauthorized testing is illegal.

### Penetration Testing Phases

```
1. Reconnaissance → 2. Scanning / Enumeration → 3. Exploitation → 4. Post-Exploitation / Lateral Movement → 5. Reporting
```

### Pentest Knowledge Levels

| Type | Tester Knowledge | Simulates |
|------|-----------------|-----------|
| **Black Box** | No prior knowledge | External attacker with no insider access |
| **White Box** | Full access to architecture, source code, credentials | Internal attacker or deep review scenario |
| **Gray Box** | Partial knowledge (e.g., a network diagram) | Partially trusted insider or partner |

---

## 5.6 Security Awareness Practices
*Given a scenario, implement security awareness practices.*

### Building a Security Culture

Security awareness transforms employees from a vulnerability into a **human firewall**. A strong program includes recurring training, simulated attacks, and reinforcement mechanisms.

### Awareness Program Components

| Component | Purpose | Best Practice |
|-----------|---------|--------------|
| **Security Awareness Training** | Educate employees on threats, policies, and safe behaviors | Annual mandatory training + role-specific modules |
| **Phishing Simulations** | Test employees' ability to recognize and report phishing | Regular, unannounced campaigns; track click rates; provide immediate feedback |
| **Policy Acknowledgment** | Formal sign-off on AUP and security policies | At onboarding and annually; creates accountability |
| **User Guidance / Job Aids** | Quick reference materials for common security tasks | Posters, one-pagers, screensavers reinforcing key messages |
| **Reporting Culture** | Encourage and streamline incident reporting | Remove fear of punishment for good-faith reports; recognize reporters |
| **Role-Based Training** | Tailored content for high-risk roles | Developers: secure coding; executives: BEC and social engineering |

### Social Engineering Defense
- Train employees to **verify identity** before acting on requests — especially those involving money, credentials, or access
- Implement a **callback verification** process for requests received via email or phone
- Make it easy to report suspicious contact without judgment

> **Exam Tip:** The single most effective technical control to stop phishing is MFA — even if credentials are stolen, the attacker cannot authenticate. The single most effective human control is a **well-trained workforce** that recognizes and reports suspicious messages.

---

## Study Checklist

### 5.1 Security Governance
- [ ] Distinguish policy, standard, procedure, and guideline — know which are mandatory
- [ ] Explain the roles of data owner, data custodian, and data steward
- [ ] List six common organizational security policies and the purpose of each
- [ ] Explain how security governance aligns the security program with business objectives

### 5.2 Risk Management Process
- [ ] Recall the risk management lifecycle steps in order
- [ ] Define threat, vulnerability, risk, likelihood, impact, residual risk, and risk appetite
- [ ] Compare the four risk response strategies: mitigation, transfer, acceptance, avoidance
- [ ] Calculate ALE given ARO and SLE
- [ ] Distinguish quantitative and qualitative risk analysis

### 5.3 Third-Party Risk Management
- [ ] Explain the purpose of NDA, MOU, MSA, SOW, SLA, and BPA
- [ ] Describe the vendor due diligence process
- [ ] Explain what a right-to-audit clause provides
- [ ] Identify why supply chain attacks target third parties

### 5.4 Security Compliance
- [ ] Match GDPR, HIPAA, PCI DSS, SOX, and ISO 27001 to their scope and key requirement
- [ ] Define PII, PHI, data subject, data controller, and data processor
- [ ] Explain the GDPR's 72-hour breach notification requirement

### 5.5 Audits and Assessments
- [ ] Distinguish internal audits from external audits
- [ ] Explain the difference between a vulnerability assessment and a penetration test
- [ ] Describe black box, white box, and gray box penetration testing
- [ ] List the five phases of a penetration test
- [ ] Explain what a red team exercise evaluates

### 5.6 Security Awareness Practices
- [ ] List the key components of a security awareness program
- [ ] Explain the value of phishing simulations and how they should be structured
- [ ] Describe role-based training and give examples of role-specific content
- [ ] Explain why a reporting culture is a critical part of the security program
