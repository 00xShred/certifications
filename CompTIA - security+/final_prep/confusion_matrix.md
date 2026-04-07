# SY0-701 Commonly Confused Terms
**Final Prep Reference**

CompTIA regularly uses similar-sounding concepts as distractors. Master these distinctions before exam day.

---

## 1. BIA vs. Risk Assessment

| | Business Impact Analysis (BIA) | Risk Assessment |
|---|---|---|
| **Focus** | Consequences of an operational disruption | Likelihood and impact of a specific threat |
| **Key Question** | "How long can the business survive without this function?" | "What is the probability and cost of this threat occurring?" |
| **Output** | MTD, RTO, RPO, critical function prioritization | Risk register, risk scores, treatment decisions |
| **When Used** | Business continuity / DR planning | Security program and risk management planning |

---

## 2. RTO vs. RPO

| | Recovery Time Objective (RTO) | Recovery Point Objective (RPO) |
|---|---|---|
| **Measures** | **Downtime** — how long you can be without service | **Data loss** — how old restored data can be |
| **Key Question** | "How fast must we recover?" | "How much data loss is acceptable?" |
| **Example** | RTO = 4 hours → service must be restored within 4 hours | RPO = 1 hour → backups must run every hour |
| **Drives** | Choice of recovery site (hot/warm/cold) | Backup frequency |

> RPO drives backup strategy. RTO drives recovery site strategy.

---

## 3. Symmetric vs. Asymmetric Encryption

| | Symmetric | Asymmetric |
|---|---|---|
| **Keys** | One shared secret key | Key pair: public + private |
| **Speed** | Fast | Slow |
| **Key distribution** | Problem — must share securely first | No problem — public key is freely distributable |
| **Primary use** | Bulk data encryption | Key exchange, digital signatures, authentication |
| **Algorithms** | AES, 3DES, ChaCha20 | RSA, ECC, Diffie-Hellman |

> In TLS: asymmetric crypto is used to **exchange** a symmetric session key. Bulk data is encrypted symmetrically.

---

## 4. IDS vs. IPS

| | IDS (Intrusion Detection System) | IPS (Intrusion Prevention System) |
|---|---|---|
| **Mode** | Passive | Active |
| **Placement** | Out-of-band (TAP/SPAN — copy of traffic) | Inline (sits in the traffic path) |
| **Action** | Logs and alerts only; cannot block | Blocks malicious traffic in real-time |
| **Risk** | Cannot stop an attack | False positives can block legitimate traffic |

> IDS = "See and tell." IPS = "See and stop."

---

## 5. Hashing vs. Salting vs. Key Stretching

| Technique | What It Does | Purpose |
|-----------|-------------|---------|
| **Hashing** | One-way, fixed-length digest | Integrity verification; password storage |
| **Salting** | Adds unique random data to each password before hashing | Defeats rainbow tables and dictionary attacks |
| **Key Stretching** | Iteratively hashes to increase computational cost | Slows brute-force attacks (PBKDF2, bcrypt, scrypt) |

> Salting defeats pre-computation. Key stretching makes each guess expensive. Use both together.

---

## 6. Authentication vs. Authorization vs. Accounting (AAA)

| | Authentication | Authorization | Accounting |
|---|---|---|---|
| **Question** | Who are you? | What can you do? | What did you do? |
| **Mechanism** | Password, MFA, certificate | ACLs, RBAC, permissions | Audit logs, SIEM |
| **Example** | Login with username + OTP | Access granted to Finance folder only | Log entry: user accessed file at 14:32 |

---

## 7. Phishing vs. Vishing vs. Smishing vs. Pharming

| Attack | Vector | Description |
|--------|--------|-------------|
| **Phishing** | Email | Deceptive email to steal credentials or deliver malware |
| **Spear Phishing** | Email | Targeted, personalized phishing attack |
| **Vishing** | Voice / Phone | Social engineering via phone call or VoIP |
| **Smishing** | SMS | Social engineering via text message |
| **Pharming** | DNS / Host file | Silently redirects users to fraudulent sites without requiring a click |

> Pharming is distinct — the victim does not need to click a link. DNS or host file is corrupted to redirect legitimate traffic.

---

## 8. Hot Site vs. Warm Site vs. Cold Site

| | Hot Site | Warm Site | Cold Site |
|---|---|---|---|
| **Hardware** | Present and fully configured | Present; partially configured | Not present (empty facility) |
| **Data** | Continuously replicated | Periodic backups; needs recent restore | No data |
| **Recovery Time** | Minutes to hours | Hours to days | Days to weeks |
| **Cost** | Highest | Medium | Lowest |
| **Exam trap** | Often confused with cloud DR (similar RTO) | Most common real-world choice | Confused with "no infrastructure" |

---

## 9. False Positive vs. False Negative

| | False Positive | False Negative |
|---|---|---|
| **Definition** | System alerts on something that is NOT a threat | System fails to alert on something that IS a threat |
| **Risk** | Alert fatigue; wasted analyst time | Real threat goes undetected and unaddressed |
| **Worse outcome** | Inefficiency | **Security breach** — the worst case |
| **IDS context** | Legitimate traffic flagged as malicious | Malicious traffic not flagged at all |

> False negatives are the more dangerous outcome.

---

## 10. EDR vs. SIEM

| | EDR | SIEM |
|---|---|---|
| **Scope** | Single endpoint (deep visibility) | Enterprise-wide log aggregation and correlation |
| **Data source** | Endpoint telemetry: process, file, memory, network | All log sources: firewalls, servers, apps, EDR, cloud |
| **Primary function** | Detect, investigate, and respond to endpoint threats | Correlate events across sources; alert on patterns |
| **Analogy** | Microscope (one device, deep detail) | Periscope (entire environment, correlation view) |

---

## 11. Vulnerability Assessment vs. Penetration Test

| | Vulnerability Assessment | Penetration Test |
|---|---|---|
| **Action** | Identifies and catalogs vulnerabilities (does not exploit) | Actively exploits vulnerabilities to prove impact |
| **Authorization needed** | Yes | Yes (plus formal rules of engagement) |
| **Output** | List of vulnerabilities with severity scores | Proof-of-concept exploits + remediation guidance |
| **Risk to target** | Low | Moderate (can cause disruption if not scoped carefully) |

---

## 12. Risk Transfer vs. Risk Mitigation vs. Risk Acceptance vs. Risk Avoidance

| Strategy | Action Taken | Example |
|----------|-------------|---------|
| **Mitigation** | Reduce likelihood or impact with controls | Patch the vulnerability; deploy a firewall |
| **Transfer** | Shift financial consequence to a third party | Purchase cyber liability insurance |
| **Acceptance** | Acknowledge and accept the risk as-is | Document low-severity risk; no action taken |
| **Avoidance** | Eliminate the risk by not doing the risky activity | Discontinue a vulnerable legacy application |

> Transfer does not eliminate the risk — only the financial consequence of that risk.

---

## 13. Data Masking vs. Tokenization

| | Data Masking | Tokenization |
|---|---|---|
| **Output** | Realistic but fictional substitute data | Meaningless random token |
| **Reversible** | Typically no | Yes — via a secure token vault |
| **Use case** | Non-production (dev, test, QA) | Production (reduces PCI DSS scope) |
| **Relation to original** | No link preserved | Token maps back to real value in vault |

---

## 14. MOU vs. MSA vs. SOW vs. SLA

| Agreement | Binding | Purpose |
|-----------|---------|---------|
| **MOU** | No | Expresses shared intent; precedes formal contracts |
| **MSA** | Yes | Overarching contract terms for an ongoing vendor relationship |
| **SOW** | Yes | Specific deliverables, timeline, and scope for a single project |
| **SLA** | Yes | Minimum service levels (uptime, response times) the provider must meet |
