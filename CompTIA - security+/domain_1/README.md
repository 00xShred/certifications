# Domain 1.0: General Security Concepts
**CompTIA Security+ SY0-701 | Exam Weight: ~12%**

This domain establishes the foundational vocabulary and concepts underlying all other security domains. Every subsequent topic builds on what is covered here.

---

## Table of Contents
- [Acronyms Quick Reference](#acronyms-quick-reference)
- [1.1 Security Controls](#11-security-controls)
- [1.2 Fundamental Security Concepts](#12-fundamental-security-concepts)
- [1.3 Change Management](#13-change-management)
- [1.4 Cryptographic Solutions](#14-cryptographic-solutions)
- [Study Checklist](#study-checklist)

---

## Acronyms Quick Reference

| Acronym | Full Term | Quick Context |
|---------|-----------|---------------|
| **CIA** | Confidentiality, Integrity, Availability | Core security triad |
| **AAA** | Authentication, Authorization, Accounting | Access control framework |
| **PKI** | Public Key Infrastructure | Certificate and key management system |
| **CA** | Certificate Authority | Issues and signs digital certificates |
| **CRL** | Certificate Revocation List | List of revoked certificates published by a CA |
| **OCSP** | Online Certificate Status Protocol | Real-time certificate revocation check |
| **CSR** | Certificate Signing Request | Sent to a CA to obtain a certificate |
| **TPM** | Trusted Platform Module | Hardware chip for cryptographic key storage and attestation |
| **HSM** | Hardware Security Module | Physical device for cryptographic operations and key protection |
| **AES** | Advanced Encryption Standard | Symmetric block cipher (128/192/256-bit) — current standard |
| **DES** | Data Encryption Standard | Legacy symmetric cipher — cryptographically broken, deprecated |
| **3DES** | Triple DES | Applies DES cipher three times — being phased out |
| **RSA** | Rivest-Shamir-Adleman | Asymmetric algorithm for encryption and digital signatures |
| **ECC** | Elliptic Curve Cryptography | Asymmetric; strong security with smaller key sizes |
| **DH** | Diffie-Hellman | Key exchange protocol; establishes shared secret over public channel |
| **HMAC** | Hash-based Message Authentication Code | Integrity + authenticity using a cryptographic hash and a secret key |
| **MD5** | Message Digest 5 | 128-bit hash — cryptographically broken, do not use for security |
| **SHA** | Secure Hash Algorithm | Family: SHA-1 (deprecated), SHA-2 (current), SHA-3 |

---

## 1.1 Security Controls
*Compare and contrast various types of security controls.*

Security controls are organized along **two axes**: the **category** of the control (how it is implemented) and its **type** (what it is designed to accomplish).

### Control Categories

| Category | Definition | Examples |
|----------|------------|---------|
| **Technical** | Implemented via technology | Firewalls, encryption, IDS/IPS, antivirus, MFA |
| **Managerial** | Implemented via policy and administrative oversight | Risk assessments, security policies, hiring background checks |
| **Operational** | Implemented by people in day-to-day procedures | Security awareness training, access badge procedures, change management |
| **Physical** | Implemented via physical barriers or mechanisms | Locks, fences, mantraps, security cameras, guards |

### Control Types (Functional Purpose)

| Type | Goal | Real-World Examples |
|------|------|---------------------|
| **Preventive** | Stop an incident before it occurs | Firewall, encryption, access control lists |
| **Detective** | Identify that an incident has occurred | IDS, audit logs, SIEM alerts, security cameras (reviewed after the fact) |
| **Corrective** | Restore systems and reduce damage after an incident | Backups, patch management, incident response procedures |
| **Deterrent** | Discourage would-be attackers | Warning signs, visible cameras, legal notices, security lighting |
| **Compensating** | Alternative control used when the primary is not feasible | Increased monitoring when a critical patch cannot be applied immediately |
| **Directive** | Specify required behavior through documentation and policy | Security policies, acceptable use policies, standard operating procedures |

> **Exam Tip:** A single control can satisfy multiple categories and types simultaneously. A visible security camera is **Physical** (category) and **Detective** (type) — and also **Deterrent**. Security awareness training is primarily an **Operational** control (carried out by people in daily practice), though some references categorize it as Managerial. Focus on understanding the *reasoning*, not just memorizing the label.

---

## 1.2 Fundamental Security Concepts
*Summarize fundamental security concepts.*

### The CIA Triad

The foundational model for all information security decisions.

| Pillar | Definition | Threatened By | Example Controls |
|--------|------------|---------------|-----------------|
| **Confidentiality** | Prevent unauthorized disclosure of information | Eavesdropping, data theft, shoulder surfing | Encryption, access control, data classification |
| **Integrity** | Prevent unauthorized modification of information | Tampering, man-in-the-middle, corruption | Hashing, digital signatures, file integrity monitoring |
| **Availability** | Ensure timely access to information and systems for authorized users | DoS/DDoS, hardware failure, ransomware | Redundancy, backups, UPS, load balancing |

### The AAA Framework

| Component | Question Answered | Examples |
|-----------|------------------|---------|
| **Authentication** | Who are you? | Passwords, MFA, biometrics, smart cards, certificates |
| **Authorization** | What are you permitted to do? | ACLs, RBAC, permissions, file system rights |
| **Accounting** | What did you do? | Audit logs, SIEM, NetFlow records |

### Additional Core Concepts

**Non-repudiation:** The inability of a party to deny having sent a message or performed an action. Achieved through **digital signatures** using asymmetric cryptography — the sender's private key signs the data, proving origin.

**Gap Analysis:** A structured comparison of the organization's current security posture against a target state or recognized standard (e.g., NIST CSF, ISO/IEC 27001). Identifies deficiencies and informs remediation priority.

**Zero Trust:** A security model built on the principle of *never trust, always verify*. No user, device, or application receives implicit trust based solely on network location. Core principles:
- **Verify explicitly** — authenticate and authorize every request using all available data
- **Use least privilege** — limit access to only what is needed
- **Assume breach** — design systems to limit blast radius and detect compromise quickly

> **Exam Tip:** Non-repudiation is tightly bound to **digital signatures**. If a question asks which technology provides non-repudiation, the answer is digital signatures. Symmetric encryption alone does not provide non-repudiation because the shared key means either party could have created the message.

---

## 1.3 Change Management
*Explain the importance of change management processes and the impact to security.*

Uncontrolled changes are a leading cause of security incidents and outages. A formal change management process ensures every change is reviewed, approved, tested, and documented before implementation.

### Key Change Management Components

| Component | Purpose |
|-----------|---------|
| **Request for Change (RFC)** | Formal document initiating a proposed change; includes description, justification, and risk |
| **Change Advisory Board (CAB)** | Review body that evaluates and approves or rejects RFCs |
| **Ownership** | Designated individual accountable for the change from approval through completion |
| **Impact Analysis** | Assessment of potential consequences — security, performance, dependencies, downstream systems |
| **Test Results** | Documented evidence that the change was validated in a non-production environment |
| **Backout Plan** | Documented procedure to revert the change if it causes problems; mandatory for every change |
| **Maintenance Window** | Pre-scheduled time for changes to minimize operational impact |
| **Change Log / Documentation** | Permanent record of what changed, when, by whom, and why; supports auditing and troubleshooting |

### Common Change Management Pitfalls (Exam Scenarios)
- Implementing a change without a backout plan → violation of change management policy
- Making an emergency change without documenting it → untracked modification, audit failure
- Skipping the CAB for "minor" changes → unauthorized change

> **Exam Tip:** The **backout plan** is consistently tested. Every change, no matter how small, must have a documented method for reverting if something goes wrong. A scenario describing a failed upgrade with no path to revert is a change management failure.

---

## 1.4 Cryptographic Solutions
*Explain the importance of using appropriate cryptographic solutions.*

### Symmetric vs. Asymmetric Encryption

| Attribute | Symmetric | Asymmetric |
|-----------|-----------|------------|
| **Key Count** | One shared secret key | Key pair: public key + private key |
| **Speed** | Fast — suitable for bulk data | Slow — not used for large data volumes |
| **Primary Use** | Data encryption (at rest and in transit session data) | Key exchange, digital signatures, authentication |
| **Key Distribution Problem** | Yes — key must be shared securely before use | No — public key can be distributed freely |
| **Common Algorithms** | AES, 3DES, ChaCha20 | RSA, ECC, Diffie-Hellman |

> **How TLS works:** Asymmetric cryptography is used to securely exchange a symmetric session key. All bulk data is then encrypted with the faster symmetric key — the best of both worlds.

### Cryptographic Concepts

| Concept | Definition | Purpose / Exam Focus |
|---------|------------|---------------------|
| **Hashing** | One-way transformation producing a fixed-length digest | Integrity — verifying data has not been altered (SHA-256, SHA-3) |
| **Salting** | Random data appended to input before hashing | Defeats rainbow table and dictionary attacks against stored passwords |
| **Digital Signatures** | Message hash encrypted with the sender's **private key** | Authentication + integrity + **non-repudiation** |
| **Key Stretching** | Iterative hashing to increase computational cost of cracking | Protects stored passwords: PBKDF2, bcrypt, scrypt |
| **Steganography** | Hiding data within non-secret media (images, audio, video) | Covert communication; also a data exfiltration technique |
| **Obfuscation** | Making data or code difficult to interpret | Reduces attacker's understanding; not true confidentiality |

### Public Key Infrastructure (PKI)

PKI is the trust framework for managing digital certificates and public-key encryption.

| Component | Role |
|-----------|------|
| **Certificate Authority (CA)** | Issues, signs, and manages digital certificates |
| **Registration Authority (RA)** | Verifies identity on behalf of the CA before a cert is issued |
| **Certificate Signing Request (CSR)** | Message from an applicant to a CA containing the public key and identity info |
| **Certificate Revocation List (CRL)** | Periodically published list of revoked certificates |
| **OCSP** | Real-time, online revocation check; preferred over CRL for freshness |
| **Certificate Pinning** | Application hardcodes the expected certificate or public key; prevents MITM |
| **TPM** | Hardware chip providing key storage, attestation, and platform integrity measurement |
| **HSM** | Dedicated hardware appliance for high-assurance cryptographic operations and key management |

### Encryption vs. Signing — Critical Distinction

| Operation | Key Used | Purpose |
|-----------|----------|---------|
| **Encrypt a message** | Recipient's **public** key | Only the recipient (private key holder) can decrypt |
| **Decrypt a message** | Recipient's **private** key | Unlocks data encrypted with the corresponding public key |
| **Sign a message** | Sender's **private** key | Proves origin; anyone with sender's public key can verify |
| **Verify a signature** | Sender's **public** key | Confirms the signature was made by the private key holder |

---

## Study Checklist

### 1.1 Security Controls
- [ ] Differentiate all four control **categories**: Technical, Managerial, Operational, Physical
- [ ] Define all six control **types**: Preventive, Detective, Corrective, Deterrent, Compensating, Directive
- [ ] Given a scenario, correctly classify a control by both category and type
- [ ] Recognize that a single control can satisfy multiple categories and types simultaneously

### 1.2 Fundamental Security Concepts
- [ ] Explain each pillar of the CIA Triad and provide an example threat and control for each
- [ ] Distinguish Authentication, Authorization, and Accounting with concrete examples
- [ ] Explain how digital signatures provide non-repudiation (and why symmetric encryption does not)
- [ ] Describe the three core principles of the Zero Trust model
- [ ] Explain the purpose of a gap analysis and give an example target standard

### 1.3 Change Management
- [ ] List the steps of a formal change management process (RFC → CAB → testing → implementation → documentation)
- [ ] Explain why a backout plan is mandatory for every change
- [ ] Identify what information must be captured in a change log
- [ ] Recognize common change management failures in exam scenarios

### 1.4 Cryptographic Solutions
- [ ] Compare symmetric and asymmetric encryption: key count, speed, and use cases
- [ ] Identify AES as the current symmetric standard (128, 192, 256-bit)
- [ ] Name primary asymmetric algorithms: RSA, ECC, Diffie-Hellman
- [ ] Explain hashing, salting, and key stretching in the context of password security
- [ ] Describe how digital signatures work: private key signs, public key verifies
- [ ] Explain the role of CA, RA, CRL, OCSP, and CSR in PKI
- [ ] Distinguish TPM (hardware chip on motherboard) from HSM (dedicated external appliance)
- [ ] Explain the difference between encrypting (for confidentiality) and signing (for authentication/integrity)
