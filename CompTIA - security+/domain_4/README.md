# Domain 4.0: Security Operations
**CompTIA Security+ SY0-701 | Exam Weight: ~28%**

The highest-weighted domain. Covers day-to-day security operations including endpoint protection, vulnerability management, identity management, incident response, and forensic investigation. Expect the most scenario-based questions from this domain.

---

## Table of Contents
- [Acronyms Quick Reference](#acronyms-quick-reference)
- [4.1 Computing Resource Security](#41-computing-resource-security)
- [4.2 Asset Management](#42-asset-management)
- [4.3 Vulnerability Management](#43-vulnerability-management)
- [4.4 Security Alerting and Monitoring](#44-security-alerting-and-monitoring)
- [4.5 Enterprise Capabilities](#45-enterprise-capabilities)
- [4.6 Identity and Access Management (IAM)](#46-identity-and-access-management-iam)
- [4.7 Automation and Orchestration](#47-automation-and-orchestration)
- [4.8 Incident Response](#48-incident-response)
- [4.9 Data Sources for Investigation](#49-data-sources-for-investigation)
- [Study Checklist](#study-checklist)

---

## Acronyms Quick Reference

| Acronym | Full Term | Quick Context |
|---------|-----------|---------------|
| **MDM** | Mobile Device Management | Centralized control and enforcement of policy on mobile devices |
| **BYOD** | Bring Your Own Device | Employee-owned device used for work; org has limited control |
| **COPE** | Corporate-Owned, Personally Enabled | Company-owned device; employee may also use it personally |
| **CYOD** | Choose Your Own Device | Employee selects from a company-approved device list |
| **NAC** | Network Access Control | Enforces security policy compliance before allowing network access |
| **EDR** | Endpoint Detection and Response | Deep endpoint visibility; behavioral detection and response |
| **XDR** | Extended Detection and Response | Cross-layer detection integrating endpoint, network, cloud, and email |
| **DLP** | Data Loss Prevention | Prevents unauthorized exfiltration of sensitive data |
| **SIEM** | Security Information and Event Management | Centralized log aggregation, correlation, and alerting |
| **SOAR** | Security Orchestration, Automation, and Response | Automated playbook execution in response to security events |
| **CVSS** | Common Vulnerability Scoring System | 0–10 severity score for vulnerabilities |
| **CVE** | Common Vulnerabilities and Exposures | Unique identifier for publicly disclosed vulnerabilities |
| **OSINT** | Open-Source Intelligence | Intelligence gathered from publicly available sources |
| **SCAP** | Security Content Automation Protocol | Standard enabling automated vulnerability management and compliance checks |
| **SAML** | Security Assertions Markup Language | XML-based standard for exchanging authentication and authorization data (used in SSO/federation) |
| **SSO** | Single Sign-On | One authentication event grants access to multiple systems |
| **MFA** | Multi-Factor Authentication | Requires two or more distinct authentication factors |
| **RBAC** | Role-Based Access Control | Access granted based on a user's assigned organizational role |
| **ABAC** | Attribute-Based Access Control | Access granted based on user, resource, and environment attributes |
| **PAM** | Privileged Access Management | Manages, monitors, and secures administrative credentials |
| **IRT** | Incident Response Team | Group responsible for executing the incident response plan |

---

## 4.1 Computing Resource Security
*Given a scenario, apply common security techniques to computing resources.*

### Hardening

Hardening reduces a system's attack surface by eliminating unnecessary functionality.

**Common hardening actions:**
- Disable or remove unnecessary services and software
- Close unused ports and protocols
- Change default credentials
- Apply vendor security benchmarks (CIS Benchmarks, DISA STIGs)
- Enable host-based firewalls and logging
- Enforce application allowlisting

### Mobile Device Management (MDM) Models

| Model | Device Owner | Org Control Level | Key Consideration |
|-------|-------------|-------------------|-------------------|
| **BYOD** (Bring Your Own Device) | Employee | Low | Privacy vs. security tension; containerization recommended |
| **COPE** (Corporate-Owned, Personally Enabled) | Organization | High | Org owns device; employee may use it for personal tasks |
| **CYOD** (Choose Your Own Device) | Organization | High | Employee selects from approved list; org manages the device |
| **COBO** (Corporate-Owned, Business Only) | Organization | Highest | Device restricted strictly to business use |

**MDM capabilities:** Remote wipe, passcode enforcement, encryption requirement, application management, geo-fencing, camera disable, containerization.

### Endpoint Security Tools

| Tool | Function |
|------|----------|
| **EDR** | Behavioral monitoring, threat detection, investigation, and automated or analyst-driven response on endpoints |
| **XDR** | Extends EDR with telemetry from email, network, and cloud — unified detection across the attack surface |
| **HIPS** | Host-based intrusion prevention; blocks suspicious behavior on a single host |
| **Antivirus / Anti-malware** | Signature-based (known threats) and heuristic (unknown threats) malware detection |
| **DLP Agent** | Monitors and controls data movement from endpoints (email, USB, cloud upload) |

### IoT / Embedded Device Security Considerations
- Limited or no patch mechanism — firmware updates may require physical access
- Default credentials frequently unchanged
- Communicate on legacy/unencrypted protocols
- Should be placed on isolated network segments (IoT VLAN)

---

## 4.2 Asset Management
*Explain the security implications of proper hardware, software, and data asset management.*

### Asset Lifecycle Stages

| Stage | Activity | Security Relevance |
|-------|----------|-------------------|
| **Procurement** | Acquire hardware/software | Verify supply chain integrity; avoid counterfeit components |
| **Inventory / Tracking** | Maintain accurate asset register | Untracked assets cannot be patched, monitored, or controlled |
| **Classification** | Categorize by sensitivity and criticality | Drives appropriate controls, handling, and disposal procedures |
| **Operation** | Monitor, patch, and maintain assets | Ongoing vulnerability management |
| **Disposal** | Sanitize or destroy at end-of-life | Prevent data recovery from discarded media |

### Data Sanitization and Disposal Methods

| Method | Description | Use Case |
|--------|-------------|---------|
| **Overwriting (Clearing)** | Writes new data patterns over existing data | Standard disposal of reusable media |
| **Degaussing** | Exposes magnetic media to a powerful magnetic field | HDDs and magnetic tapes; renders media unusable |
| **Cryptographic Erase** | Destroys the encryption key for a fully encrypted drive | SSDs and encrypted volumes; effectively unrecoverable |
| **Physical Destruction** | Shredding, pulverizing, incineration | Highest assurance; no reuse possible |

**Data Retention:** Organizations must retain data for legally or contractually mandated periods. Premature deletion may violate compliance requirements; indefinite retention increases breach exposure.

---

## 4.3 Vulnerability Management
*Explain various activities associated with vulnerability management.*

### Vulnerability Management Lifecycle

```
Identify → Assess → Prioritize → Remediate → Verify → Report → (repeat)
```

### Vulnerability Scanning Types

| Scan Type | Description |
|-----------|-------------|
| **Credentialed scan** | Scanner authenticates to the target; provides deeper visibility into installed software and config |
| **Non-credentialed scan** | External perspective only; finds exposed services and open ports |
| **Internal scan** | Run from inside the network; finds vulnerabilities attackers could exploit post-breach |
| **External scan** | Run from outside the perimeter; mirrors attacker view |
| **Agent-based scan** | Lightweight agent installed on endpoint reports data to central scanner |
| **SAST** (Static Application Security Testing) | Analyzes source code without executing it |
| **DAST** (Dynamic Application Security Testing) | Tests running application by sending inputs and observing responses |

### Vulnerability Scoring and Classification

| Standard | Purpose |
|----------|---------|
| **CVE** | Unique identifier (e.g., CVE-2021-44228 for Log4Shell) for a specific vulnerability |
| **CVSS** | Numerical severity score 0–10: Low (0–3.9), Medium (4–6.9), High (7–8.9), Critical (9–10) |
| **NVD** | NIST's National Vulnerability Database — provides CVE enrichment including CVSS scores |
| **SCAP** | Automates vulnerability checking and compliance validation |

### False Positives vs. False Negatives

| Result | Definition | Risk |
|--------|------------|------|
| **False Positive** | Vulnerability flagged that does not actually exist | Wastes remediation resources; alert fatigue |
| **False Negative** | Real vulnerability not detected by the scan | Highest risk — vulnerability remains unaddressed |

> **Exam Tip:** False negatives are the worst-case scan outcome — a real vulnerability goes undetected. Non-credentialed scans have higher false negative rates than credentialed scans because they have less visibility into the system.

---

## 4.4 Security Alerting and Monitoring
*Explain security alerting and monitoring concepts and tools.*

### SIEM

A SIEM collects, normalizes, and correlates log data from across the environment to detect security events and generate alerts.

**Key SIEM capabilities:**
- **Log aggregation** — ingests logs from firewalls, servers, endpoints, cloud, applications
- **Normalization** — converts disparate log formats into a common schema
- **Correlation** — applies rules to identify patterns across multiple log sources
- **Alerting** — notifies analysts of potential security events
- **Dashboards / Reporting** — visibility into security posture over time

### Monitoring Concepts

| Concept | Description |
|---------|-------------|
| **Continuous monitoring** | Ongoing, automated observation of systems and networks for security events |
| **Log aggregation** | Centralizing logs from all sources into a single repository for analysis |
| **Baselining** | Establishing normal behavior patterns; deviations trigger investigation |
| **Threat intelligence feeds** | External IOC/IOA data enriching SIEM detections (known malicious IPs, domains, hashes) |
| **User and Entity Behavior Analytics (UEBA)** | Machine learning models detecting anomalous user or device behavior |

### Alert Types and Tuning

Alerts should be tuned to reduce **false positives** (alert fatigue) while ensuring **true positives** are not missed. Effective alerting requires:
- Clear severity tiers (Critical, High, Medium, Low)
- Documented response procedures (playbooks) for each alert type
- Regular review and tuning of correlation rules

---

## 4.5 Enterprise Capabilities
*Given a scenario, modify enterprise capabilities to enhance security.*

### Network-Level Controls

| Control | Purpose | Example |
|---------|---------|---------|
| **Firewall Rules** | Permit or deny traffic based on source, destination, port, and protocol | Block inbound RDP (3389) from internet; allow only from jump server |
| **ACLs** | Fine-grained traffic filtering at router or switch level | Restrict VLAN-to-VLAN communications |
| **NAC (Network Access Control)** | Enforce security posture compliance before granting network access | Require current AV and OS patches; quarantine non-compliant devices |
| **DNS Filtering** | Block resolution of known malicious domains | Prevents connections to C2 servers and phishing sites |
| **Web Proxy / Content Filtering** | Intercepts and inspects HTTP/S traffic; enforces acceptable use policy | Block social media, inspect HTTPS via TLS inspection |
| **WAF** | Filters application-layer HTTP/S attacks | Blocks SQLi, XSS, CSRF targeting web applications |

> **Exam Tip:** **NAC** evaluates device health (patch level, AV status, certificate) **before** granting access — it is a pre-admission control. Compare to a firewall, which is a perimeter control for traffic that has already been admitted.

---

## 4.6 Identity and Access Management (IAM)
*Given a scenario, implement and maintain identity and access management.*

### IAM Lifecycle

| Phase | Activities |
|-------|-----------|
| **Provisioning** | Create user account; assign roles, groups, and minimum required permissions |
| **Modification** | Update access when role changes (job transfer, promotion) |
| **De-provisioning** | Disable/delete account promptly when employment ends |
| **Access Review** | Periodic certification that existing access is still appropriate |

### Authentication Factors

| Factor Category | Examples |
|----------------|---------|
| **Something you know** | Password, PIN, security question |
| **Something you have** | Smart card, hardware token (TOTP), OTP via SMS |
| **Something you are** | Fingerprint, retina scan, facial recognition (biometrics) |
| **Somewhere you are** | Geolocation, IP address restriction |

**MFA** combines at least **two different factor categories**. Two passwords = not MFA.

### Access Control Models

| Model | Description | Example |
|-------|-------------|---------|
| **RBAC** (Role-Based) | Access determined by the user's assigned role | "Finance" role grants read access to budget system |
| **ABAC** (Attribute-Based) | Access based on attributes of user, resource, and environment | "Cleared for Top Secret" AND "location = HQ" AND "time = business hours" |
| **DAC** (Discretionary) | Resource owner controls access | File owner sets permissions on their own files |
| **MAC** (Mandatory) | Access controlled by a central authority based on labels/classifications | Government systems: Unclassified, Secret, Top Secret |
| **Rule-Based** | Access controlled by a set of administrator-defined rules | Firewall ACL rules |

### Key IAM Concepts

| Concept | Definition |
|---------|------------|
| **Least Privilege** | Users receive only the minimum access required for their job function |
| **Separation of Duties** | No single individual can complete a high-risk transaction end-to-end |
| **Mandatory Vacation** | Requiring employees to take leave to detect fraud hidden by continuous presence |
| **Job Rotation** | Periodically rotating employees through roles to detect and prevent fraud |
| **SSO** | One authentication event grants access to multiple linked applications |
| **Federation** | SSO extended across organizational boundaries using standards (SAML, OIDC) |
| **PAM** | Controls, monitors, and audits privileged (admin) account access; enforces just-in-time access |

> **Exam Tip:** **PAM** is specifically about securing **privileged/administrative** accounts. It typically includes session recording, credential vaulting, and just-in-time access provisioning. Do not confuse it with general IAM.

---

## 4.7 Automation and Orchestration
*Explain the importance of automation and orchestration related to secure operations.*

### SOAR

**SOAR** (Security Orchestration, Automation, and Response) enables security teams to define **playbooks** — step-by-step automated workflows triggered by specific alert types.

**Example SOAR playbook:** SIEM detects beaconing → SOAR automatically isolates the affected endpoint from the network → creates an incident ticket → notifies the on-call analyst.

**Benefits:**
- Reduces mean time to respond (MTTR)
- Eliminates manual steps in repetitive response tasks
- Enforces consistent response procedures
- Allows analysts to focus on high-judgment tasks

### Automation Use Cases in Security

| Use Case | Tool / Approach |
|----------|----------------|
| Vulnerability scanning | Scheduled automated scans (Nessus, Qualys) |
| Log parsing and alerting | SIEM correlation rules |
| Threat intelligence enrichment | Auto-lookup of IOCs against threat intel feeds |
| User account provisioning | Identity governance platform + HR system integration |
| Patch deployment | Automated patch management (WSUS, SCCM, Ansible) |
| Incident response | SOAR playbooks |
| Configuration compliance | SCAP, Desired State Configuration (DSC), Ansible |

### Scripting and APIs
- **Python, PowerShell, Bash** — Common scripting languages for security automation
- **APIs** — Enable integration between security tools; allow programmatic access to SIEM, EDR, ticketing systems
- **Risk of over-automation:** Scripts themselves can introduce vulnerabilities; require secure coding practices and change management

---

## 4.8 Incident Response
*Explain appropriate incident response activities.*

### Incident Response Lifecycle (NIST SP 800-61)

```
1. Preparation → 2. Detection and Analysis → 3. Containment → 4. Eradication → 5. Recovery → 6. Lessons Learned
```

| Phase | Key Activities |
|-------|---------------|
| **Preparation** | Develop IR plan, playbooks, and communication trees; train the team; deploy monitoring tools |
| **Detection and Analysis** | Identify the incident from alerts, logs, or user reports; determine scope and severity |
| **Containment** | Limit the spread — isolate affected systems (short-term then long-term containment) |
| **Eradication** | Remove the root cause — delete malware, close exploited vulnerability, reset credentials |
| **Recovery** | Restore systems from known-good state; monitor for reinfection; validate normal operation |
| **Lessons Learned** | Post-incident review; document timeline; update playbooks and controls |

### Digital Forensics Principles

| Principle | Description |
|-----------|-------------|
| **Order of Volatility** | Collect most volatile evidence first: CPU registers → RAM → swap/page file → disk → logs → archived data |
| **Chain of Custody** | Documented record of every person who handled evidence; ensures admissibility |
| **Legal Hold** | Suspension of normal data destruction policies when litigation is anticipated |
| **Write Blockers** | Hardware or software that prevents modification of evidence media during acquisition |
| **Forensic Image** | Bit-for-bit copy of storage media; analyst works from the copy, never the original |

> **Exam Tip:** **Containment before eradication** — this order matters. Containing the incident first prevents further spread and preserves evidence. Eradicating the threat before containing it can result in the attacker re-establishing access.

### IR Communication

- **Escalation path** — defined chain from analyst → IR lead → CISO → legal/executive
- **Out-of-band communication** — use alternative channels (phone, signal) if primary email/chat may be compromised
- **External notifications** — regulatory reporting requirements (e.g., GDPR 72-hour breach notification)

---

## 4.9 Data Sources for Investigation
*Given a scenario, use data sources to support an investigation.*

### Log Sources

| Log Source | What It Captures | Investigation Use |
|------------|-----------------|-------------------|
| **Firewall logs** | Permitted and denied connections with source/destination IP, port, timestamp | Identify C2 beaconing, blocked attack attempts, lateral movement |
| **System logs (OS)** | Login events, privilege use, service starts/stops, errors | Detect unauthorized access, account changes, persistence mechanisms |
| **Application logs** | Application-specific events, errors, authentication | Web server access logs reveal SQLi attempts, brute force |
| **DNS logs** | DNS queries and responses | Detect DNS tunneling, connections to malicious domains |
| **Authentication logs** | Successful and failed login events | Identify brute force, credential stuffing, account compromise |
| **IDS/IPS logs** | Detected and blocked attack signatures | Identify attack type and timing |
| **Antivirus/EDR logs** | Malware detections, behavioral alerts | Trace infection chain |

### Network Data Sources

| Source | Description | Investigation Use |
|--------|-------------|-------------------|
| **NetFlow / IPFIX** | Flow records: source/dest IP, port, bytes, duration | Traffic pattern analysis; detect beaconing, exfiltration |
| **Packet Capture (PCAP)** | Full content of network packets | Deep forensic analysis of specific sessions; must be stored and secured |
| **Wireless (802.11) logs** | AP association, SSID, channel, client MAC | Detect rogue APs, unauthorized clients |

### Other Data Sources

| Source | Description |
|--------|-------------|
| **Email headers** | Contains routing information (Received: fields), originating server IP, authentication results (SPF, DKIM, DMARC) — used to trace phishing origins |
| **Metadata** | Data about data: file creation/modification timestamps, author, GPS coordinates in images |
| **Vulnerability scanner output** | Current vulnerability state of systems at the time of the incident |
| **Threat intelligence** | External IOC feeds cross-referenced against observed indicators |

> **Exam Tip — Order of Volatility:** Always preserve the most volatile data first. RAM contents (running processes, encryption keys, network connections) are lost when a system is powered off. Disk data persists but can be modified. Acquire in this order: RAM → disk image → network logs → archived data.

---

## Study Checklist

### 4.1 Computing Resource Security
- [ ] List at least five hardening actions applicable to a new server or workstation
- [ ] Compare BYOD, COPE, CYOD, and COBO in terms of organizational control
- [ ] Explain what MDM capabilities are used to secure mobile devices (remote wipe, encryption, geo-fence)
- [ ] Distinguish EDR from XDR in scope of visibility
- [ ] Identify IoT-specific security challenges

### 4.2 Asset Management
- [ ] List the stages of the asset lifecycle
- [ ] Distinguish overwriting, degaussing, cryptographic erase, and physical destruction
- [ ] Explain the purpose of data retention policies

### 4.3 Vulnerability Management
- [ ] Explain the vulnerability management lifecycle
- [ ] Distinguish credentialed vs. non-credentialed scans
- [ ] Explain CVSS scoring (0–10 scale) and CVE identifiers
- [ ] Define false positive and false negative; identify which is more dangerous in vulnerability scanning

### 4.4 Security Alerting and Monitoring
- [ ] Explain the role of a SIEM and list four capabilities (aggregation, normalization, correlation, alerting)
- [ ] Describe how baselining supports anomaly detection
- [ ] Explain the impact of alert fatigue and how tuning addresses it

### 4.5 Enterprise Capabilities
- [ ] Explain how NAC enforces device health compliance before granting network access
- [ ] Describe the role of DNS filtering in blocking C2 communications
- [ ] Explain the difference between a firewall rule and an ACL

### 4.6 Identity and Access Management
- [ ] Describe the complete IAM lifecycle: provisioning → modification → de-provisioning → access review
- [ ] List the three primary authentication factor categories with examples of each
- [ ] Distinguish RBAC, ABAC, DAC, and MAC with concrete examples
- [ ] Explain least privilege, separation of duties, mandatory vacation, and job rotation
- [ ] Explain SSO, federation, and PAM

### 4.7 Automation and Orchestration
- [ ] Explain what SOAR does and describe a sample playbook
- [ ] List three benefits of security automation
- [ ] Identify common scripting languages used in security operations

### 4.8 Incident Response
- [ ] Recall all six phases of the NIST incident response lifecycle in order
- [ ] Explain why containment comes before eradication
- [ ] Define chain of custody, legal hold, order of volatility, and forensic imaging
- [ ] Describe the purpose of write blockers in forensic investigations

### 4.9 Data Sources for Investigation
- [ ] Match log source types to the investigation questions they answer
- [ ] Explain the difference between NetFlow and packet capture
- [ ] Describe what information can be extracted from email headers
- [ ] Recall the order of volatility for evidence collection
