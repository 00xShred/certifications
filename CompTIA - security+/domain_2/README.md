# Domain 2.0: Threats, Vulnerabilities, and Mitigations
**CompTIA Security+ SY0-701 | Exam Weight: ~22%**

The second highest-weighted domain. Focuses on recognizing attack types, understanding how vulnerabilities arise, and applying the right mitigation strategies. Expect heavy scenario-based question coverage.

---

## Table of Contents
- [Acronyms Quick Reference](#acronyms-quick-reference)
- [2.1 Threat Actors and Motivations](#21-threat-actors-and-motivations)
- [2.2 Threat Vectors and Attack Surfaces](#22-threat-vectors-and-attack-surfaces)
- [2.3 Vulnerabilities](#23-vulnerabilities)
- [2.4 Indicators of Malicious Activity](#24-indicators-of-malicious-activity)
- [2.5 Mitigation Techniques](#25-mitigation-techniques)
- [Study Checklist](#study-checklist)

---

## Acronyms Quick Reference

| Acronym | Full Term | Quick Context |
|---------|-----------|---------------|
| **APT** | Advanced Persistent Threat | Nation-state or state-sponsored long-term, stealthy campaign |
| **CVE** | Common Vulnerabilities and Exposures | Standard identifier for publicly disclosed vulnerabilities |
| **CVSS** | Common Vulnerability Scoring System | 0–10 severity score for vulnerabilities |
| **DDoS** | Distributed Denial of Service | Multi-source availability attack |
| **DNS** | Domain Name System | Target for poisoning, tunneling, hijacking |
| **OSINT** | Open-Source Intelligence | Passive reconnaissance from publicly available sources |
| **SQLi** | SQL Injection | Unsanitized input exploited to manipulate a database |
| **XSS** | Cross-Site Scripting | Malicious scripts injected into web pages and run in other users' browsers |
| **SIEM** | Security Information and Event Management | Log aggregation and correlation platform |
| **DLP** | Data Loss Prevention | Prevents unauthorized data exfiltration |
| **IPS** | Intrusion Prevention System | Active, inline threat blocking |
| **IDS** | Intrusion Detection System | Passive, out-of-band; alerts only |
| **MSSP** | Managed Security Service Provider | Outsourced security monitoring and management |
| **RAT** | Remote Access Trojan | Malware providing covert remote control to attacker |
| **SOC** | Security Operations Center | Centralized team for security monitoring and response |
| **XDR** | Extended Detection and Response | Cross-layer detection and response platform |
| **SOAR** | Security Orchestration, Automation, and Response | Automated security workflow execution and response |

---

## 2.1 Threat Actors and Motivations
*Compare and contrast common threat actors and motivations.*

### Threat Actor Types

| Actor Type | Resources / Skill | Primary Motivations | Distinguishing Characteristics |
|------------|------------------|---------------------|---------------------------------|
| **Nation-State** | Very high; state-funded | Espionage, sabotage, geopolitical disruption | Long dwell time, stealth; the source of most APTs |
| **Organized Crime** | High; well-funded | Financial gain | Ransomware, card theft, fraud, BEC |
| **Hacktivist** | Variable | Ideological, political, or social causes | Public embarrassment, DDoS, website defacement |
| **Insider Threat** | Varies; has authorized access | Financial gain, revenge, coercion, negligence | Hardest to detect; legitimate credentials in use |
| **Unskilled Attacker (Script Kiddie)** | Low | Curiosity, notoriety | Uses off-the-shelf tools; limited understanding of underlying techniques |
| **Competitor** | Variable | Corporate espionage | Intellectual property theft, competitive intelligence |

> **Exam Tip — APT vs. Organized Crime:** **APT (Advanced Persistent Threat)** is specifically associated with **nation-state or state-sponsored** actors conducting long-term, stealthy campaigns with strategic objectives. Financially motivated organized crime groups — even sophisticated ones — are **not** APTs. This distinction is frequently tested.

### Common Threat Actor Motivations

| Motivation | Actor Types |
|-----------|------------|
| **Data exfiltration** | Nation-state, organized crime, insider |
| **Financial gain** | Organized crime, insider, unskilled attackers |
| **Espionage / intelligence gathering** | Nation-state, competitor |
| **Service disruption** | Nation-state, hacktivist |
| **Blackmail / extortion** | Organized crime |
| **Ideological / philosophical** | Hacktivist |
| **Revenge** | Insider |

### Shadow IT
**Shadow IT** — the use of unauthorized applications, cloud services, or devices without IT department knowledge or approval. Expands the attack surface and introduces unmanaged, unpatched, and potentially misconfigured resources.

---

## 2.2 Threat Vectors and Attack Surfaces
*Explain common threat vectors and attack surfaces.*

### Social Engineering Attacks

| Attack | Primary Vector | Description |
|--------|---------------|-------------|
| **Phishing** | Email | Mass or targeted deceptive message to steal credentials or deliver malware |
| **Spear Phishing** | Email | Targeted phishing against a specific individual or organization; highly personalized |
| **Whaling** | Email | Spear phishing targeting C-suite executives or high-value individuals |
| **Vishing** | Voice / Phone | Social engineering via phone or VoIP call |
| **Smishing** | SMS | Social engineering via text message |
| **Pretexting** | Any | Fabricated backstory used to build trust and extract information or action |
| **Pharming** | DNS / Host file | Redirects users to fraudulent sites by poisoning DNS cache or modifying host files |
| **Typosquatting** | Web / Domain | Registers domain variants of popular sites to capture mistyped traffic |
| **Watering Hole** | Web | Compromises a website known to be visited by the intended target group |
| **Business Email Compromise (BEC)** | Email | Impersonates executives or vendors to authorize fraudulent transactions |

### Technical Attack Vectors

| Vector | Description | Example |
|--------|-------------|---------|
| **Email attachments** | Malware delivery via malicious Office docs, PDFs, archives | Macro-enabled Word doc deploys ransomware |
| **Image-based** | Malicious content hidden in or exploiting image file parsers | Stegoed payload or exploit in JPEG parser |
| **Removable media** | USB drives pre-loaded with malware; auto-run exploitation | Malicious USB drop in a parking lot |
| **Open service ports** | Exposed services exploitable if unpatched or misconfigured | Exposed RDP (3389) brute-forced |
| **Default credentials** | Factory username/password left unchanged on devices | `admin`/`admin` on a network switch |
| **Supply chain** | Compromising a vendor or software update to attack downstream targets | SolarWinds-style update poisoning |
| **Unsecured wireless** | Rogue APs, evil twin attacks, unencrypted traffic interception | Fake "Free WiFi" hotspot capturing credentials |

> **Exam Tip:** **Supply chain attacks** are high-impact because they exploit an established trust relationship. The attacker never needs to directly breach the target — they compromise a trusted third party (hardware vendor, software update server, or managed service provider) and ride that trust in.

---

## 2.3 Vulnerabilities
*Explain various types of vulnerabilities.*

### Application Vulnerabilities

| Vulnerability | Description | Mitigation |
|--------------|-------------|------------|
| **Buffer Overflow** | Writing beyond allocated memory boundaries, potentially overwriting adjacent memory to redirect execution | Input validation, bounds checking, ASLR, DEP/NX |
| **Memory Injection** | Injecting malicious code directly into a running process's memory space | Code signing, DEP, sandboxing, application allowlisting |
| **Race Condition / TOCTOU** | Behavior depends on timing; attacker manipulates the gap between Time of Check and Time of Use | Atomic operations, mutex/locking mechanisms |
| **SQL Injection (SQLi)** | Unsanitized user input is interpreted as SQL commands, allowing DB read/modify/delete | Parameterized queries, prepared statements, input validation |
| **Cross-Site Scripting (XSS)** | Malicious scripts injected into a trusted web page; executed in other users' browsers | Input sanitization, Content Security Policy (CSP), output encoding |
| **Cross-Site Request Forgery (CSRF)** | Tricks authenticated user's browser into making unauthorized requests | CSRF tokens, SameSite cookies |

### Other Vulnerability Categories

| Category | Key Examples |
|----------|-------------|
| **Zero-Day** | Unknown to the vendor; no patch exists; often sold on dark web or used by nation-state actors |
| **Misconfiguration** | Default credentials, unnecessary open ports, verbose error messages, world-readable cloud storage |
| **Weak / Deprecated Cryptography** | MD5, SHA-1, DES, RC4, SSLv3 — known to be breakable |
| **Hardware** | Firmware vulnerabilities, hardware implants, supply chain tampering at the chip level |
| **Virtualization** | VM escape (breaking out of hypervisor), hypervisor vulnerabilities, VM sprawl |
| **Cloud-Specific** | Misconfigured S3 buckets, over-permissive IAM roles, insecure APIs, shared tenancy risks |
| **IoT / Embedded** | No patch mechanism, default credentials, unencrypted protocols, limited compute for security |

> **Exam Tip — Zero-Day:** A zero-day is unknown to the vendor **and** unpatched. Signature-based IDS/IPS cannot detect zero-days because no signature exists. **Anomaly-based** or **behavior-based** detection is the appropriate mitigation when no patch is available.

---

## 2.4 Indicators of Malicious Activity
*Given a scenario, analyze indicators of malicious activity.*

### Malware Types and Indicators

| Malware Type | Behavior | Key Behavioral Indicators |
|-------------|----------|--------------------------|
| **Ransomware** | Encrypts victim files; demands payment for decryption key | File extension changes, ransom note, massive I/O write activity |
| **Trojan** | Disguises itself as legitimate software; delivers malicious payload | Unexpected outbound connections after new software installation |
| **RAT (Remote Access Trojan)** | Provides attacker with covert, persistent remote control | Unusual processes, webcam/mic activity, unexpected outbound sessions |
| **Rootkit** | Hides its presence and provides privileged system access | Discrepancies between OS-reported state and actual disk/memory contents |
| **Keylogger** | Records every keystroke made by the user | Credential theft, character streams transmitted to external host |
| **Botnet / Zombie** | Infected host under command-and-control (C2) server | **Beaconing** — regular, timed outbound connections to C2 IP |
| **Worm** | Self-replicates across networks without user interaction | Network flooding, rapid lateral spread, high CPU/bandwidth |
| **Spyware** | Monitors user activity without consent; transmits data | Unauthorized outbound data, browser redirects, performance degradation |
| **Fileless Malware** | Operates entirely in memory; no files written to disk | Unusual PowerShell/WMI activity, legitimate process anomalies |

### Network-Level Indicators

| Indicator | Significance |
|-----------|-------------|
| **Beaconing** | Regular, periodic outbound connections at set intervals → active C2 channel |
| **Unusual traffic volumes** | Sudden bandwidth spikes, especially outbound → data exfiltration or DDoS participation |
| **DNS tunneling** | Encoded data exfiltrated within DNS queries → bypasses standard egress controls |
| **Traffic to known-malicious IPs** | SIEM/threat intel integration catches this → IOC match |
| **Unexpected port usage** | Traffic on unusual ports or protocol mismatches → policy violation or covert channel |
| **Lateral movement patterns** | Internal host-to-host connections spreading from an initial compromise point |

### System and Application Indicators

- **Account lockouts** — brute-force or credential stuffing in progress
- **Privilege escalation events** — attacker moving from low-privilege to admin access
- **Unexpected scheduled tasks or services** — persistence mechanism installed
- **Registry modifications** (Windows) — autorun keys, service entries → persistence
- **Log clearing or modification** — attacker covering tracks; treat as active incident
- **Unexpected processes or network listeners** — unauthorized software running

> **Exam Tip:** **Beaconing** is a key C2 indicator. Regular, periodic outbound connections from an endpoint — especially to unknown or geographically unusual IPs — suggest an active botnet or RAT infection. SIEM correlation rules detect this pattern by flagging repeated connections on fixed intervals.

---

## 2.5 Mitigation Techniques
*Explain the purpose of mitigation techniques used to secure the enterprise.*

### Network-Level Mitigations

| Technique | Purpose | Key Detail |
|-----------|---------|-----------|
| **Network Segmentation** | Divides the network into security zones; limits lateral movement after breach | Implemented with firewalls, VLANs, ACLs |
| **Isolation** | Completely separates a system from all others | Used for compromised hosts (quarantine) or highly sensitive assets (air-gap) |
| **VLANs** | Logical segmentation without physical infrastructure changes | Enforces separation between departments or device types |
| **ACLs** | Define permitted/denied traffic at network or application layer | Applied on routers, firewalls, and switches |
| **Honeypot / Honeynet** | Decoy systems or networks designed to detect, study, and divert attackers | Provides early warning; slows attackers; gathers TTPs |
| **Sinkholes** | DNS sinkholing redirects C2 traffic to a controlled server | Cuts off communication between bots and their C2 |

### Endpoint Mitigations

| Technique | Purpose |
|-----------|---------|
| **Hardening** | Remove unnecessary services, disable unused ports, apply CIS benchmarks / STIGs |
| **Patch Management** | Apply security updates to address known vulnerabilities in a timely manner |
| **EDR (Endpoint Detection and Response)** | Deep endpoint visibility; behavioral detection; automated or analyst-driven response |
| **HIPS (Host-based Intrusion Prevention System)** | Monitors and blocks malicious activity on individual hosts |
| **DLP (Data Loss Prevention)** | Prevents unauthorized transfer of sensitive data via email, USB, cloud, etc. |
| **Application Allowlisting** | Only pre-approved applications may execute; blocks unknown/malicious code |

### Access Control Mitigations

| Principle | Definition | Why It Matters |
|-----------|-----------|---------------|
| **Least Privilege** | Grant only the minimum permissions required for a task | Limits damage from compromised accounts |
| **Separation of Duties** | No single person has end-to-end control over a critical process | Prevents fraud and insider abuse |
| **Permission Reviews** | Regular auditing of who has access to what | Removes stale, over-permissive, or orphaned accounts |

> **Exam Tip:** **Segmentation limits the blast radius** of a breach — it does not prevent the initial compromise. After breaching one host, an attacker must cross segment boundaries to reach other systems. Combining segmentation with least privilege access control significantly hinders lateral movement.

---

## Study Checklist

### 2.1 Threat Actors and Motivations
- [ ] Identify the six primary threat actor types and their typical resources and motivations
- [ ] Clearly distinguish APT (nation-state) from organized crime (financially motivated)
- [ ] Define Shadow IT and explain its security implications

### 2.2 Threat Vectors and Attack Surfaces
- [ ] Differentiate phishing, spear phishing, whaling, vishing, smishing, pharming, and pretexting
- [ ] Explain typosquatting and watering hole attacks
- [ ] Describe supply chain attacks and explain why they are high-impact
- [ ] Identify message-based, image-based, file-based, and removable media attack vectors
- [ ] Explain the risks of open service ports and default credentials

### 2.3 Vulnerabilities
- [ ] Explain buffer overflow and how it can lead to arbitrary code execution
- [ ] Distinguish SQL injection (server-side, DB) from XSS (client-side, browser)
- [ ] Define zero-day and explain why signature-based detection fails against it
- [ ] Identify misconfiguration as the most common and preventable vulnerability class
- [ ] Explain race conditions / TOCTOU and how locking mechanisms mitigate them

### 2.4 Indicators of Malicious Activity
- [ ] Match behavioral indicators to malware types: ransomware, rootkit, RAT, keylogger, worm
- [ ] Explain beaconing and identify it as a C2 communication indicator
- [ ] Recognize account lockouts, log clearing, and privilege escalation as attack indicators
- [ ] Understand why fileless malware is harder to detect with traditional AV

### 2.5 Mitigation Techniques
- [ ] Explain network segmentation and how it limits lateral movement
- [ ] Describe the purpose of honeypots and honeynets
- [ ] Define hardening and list at least four specific hardening actions
- [ ] Explain least privilege and separation of duties and give examples
- [ ] Compare EDR, HIPS, and DLP in terms of scope and function
