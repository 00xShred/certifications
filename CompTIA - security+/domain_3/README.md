# Domain 3.0: Security Architecture
**CompTIA Security+ SY0-701 | Exam Weight: ~18%**

Covers the design and implementation of secure infrastructure — from cloud and on-premises deployment models to network appliance placement, data protection strategies, and resilience planning.

---

## Table of Contents
- [Acronyms Quick Reference](#acronyms-quick-reference)
- [3.1 Architecture Models](#31-architecture-models)
- [3.2 Securing Enterprise Infrastructure](#32-securing-enterprise-infrastructure)
- [3.3 Protecting Data](#33-protecting-data)
- [3.4 Resilience and Recovery](#34-resilience-and-recovery)
- [Study Checklist](#study-checklist)

---

## Acronyms Quick Reference

| Acronym | Full Term | Quick Context |
|---------|-----------|---------------|
| **IaC** | Infrastructure as Code | Provision and manage infrastructure through code (Terraform, Ansible) |
| **RTOS** | Real-Time Operating System | OS for deterministic real-time processing; used in OT/ICS/IoT |
| **ICS** | Industrial Control Systems | Manages industrial operations (power grids, water treatment, manufacturing) |
| **SCADA** | Supervisory Control and Data Acquisition | High-level supervisory layer of an ICS |
| **SDN** | Software-Defined Networking | Separates the control plane from the data plane; centrally programmable |
| **SD-WAN** | Software-Defined Wide Area Network | SDN principles applied to WAN connectivity |
| **WAF** | Web Application Firewall | Filters HTTP/S traffic; protects against SQLi, XSS, and OWASP Top 10 |
| **UTM** | Unified Threat Management | Single appliance combining firewall, IDS/IPS, antivirus, DLP |
| **NGFW** | Next-Generation Firewall | Layer 7 application awareness + deep packet inspection + traditional firewall |
| **IDS** | Intrusion Detection System | Passive; out-of-band; alerts only |
| **IPS** | Intrusion Prevention System | Active; inline; blocks malicious traffic in real-time |
| **VPN** | Virtual Private Network | Encrypted tunnel over a public network |
| **TLS** | Transport Layer Security | Cryptographic protocol securing data in transit (current: TLS 1.2/1.3) |
| **IPsec** | Internet Protocol Security | Layer 3 encryption; used in site-to-site VPNs |
| **SASE** | Secure Access Service Edge | Cloud-delivered convergence of networking and security functions |
| **DLP** | Data Loss Prevention | Detects and prevents unauthorized data exfiltration |
| **UPS** | Uninterruptible Power Supply | Battery backup providing power continuity during outages |
| **CASB** | Cloud Access Security Broker | Enforces security policy between users and cloud applications |

---

## 3.1 Architecture Models
*Compare and contrast security implications of different architecture models.*

### Cloud Deployment Models

| Model | Description | Key Security Consideration |
|-------|-------------|---------------------------|
| **Public Cloud** | Multi-tenant infrastructure managed by a CSP (AWS, Azure, GCP) | Shared responsibility model — CSP secures the infrastructure; customer secures data, config, and access |
| **Private Cloud** | Dedicated infrastructure for a single organization | Customer controls all layers; highest cost; no shared tenancy risks |
| **Hybrid Cloud** | Combination of public and private cloud | Data classification determines placement; secure interconnects between environments required |
| **Multi-Cloud** | Multiple CSPs in use simultaneously | Avoids vendor lock-in; complex IAM and consistent policy enforcement is a challenge |
| **Community Cloud** | Shared among organizations with common regulatory or mission requirements | Used in government, healthcare, and financial sectors |

### Shared Responsibility Model

The CSP is responsible for security **of** the cloud (physical facilities, hardware, hypervisor, core networking). The customer is responsible for security **in** the cloud:

| CSP Responsibility | Customer Responsibility |
|--------------------|------------------------|
| Physical data centers | Data classification and encryption |
| Core infrastructure | Identity and access management |
| Hypervisor / hardware | Operating system patching (IaaS) |
| Networking fabric | Application security |
| — | Firewall and security group configuration |

> **Exam Tip:** Misconfigured cloud storage (e.g., a publicly readable S3 bucket exposing sensitive data) is a **customer** responsibility failure, not a CSP failure. The CSP's infrastructure was functioning correctly.

### Computing Architecture Types

| Type | Description | Primary Security Risk |
|------|-------------|----------------------|
| **Virtualization** | Multiple VMs on a shared physical host via a hypervisor | VM escape, hypervisor vulnerabilities, VM sprawl |
| **Containerization** | Lightweight isolated application packages (Docker, Kubernetes) | Container escape, vulnerable base images, registry security |
| **Serverless** | Function-as-a-Service; CSP manages all infrastructure | Function code security, overly permissive execution roles, event injection |
| **Microservices** | Application decomposed into independent, loosely coupled services | API security, service-to-service authentication, granular access control |
| **Infrastructure as Code (IaC)** | Infrastructure defined and provisioned via code files | Configuration drift prevention; version control and peer review of infrastructure changes |
| **Air-Gapped** | Physically isolated from all unsecured networks | Highest isolation level; data transfer via physical media introduces risk |
| **Software-Defined Networking (SDN)** | Control plane separated from data plane; centrally managed | The SDN controller is a high-value attack target |
| **OT / ICS / SCADA** | Operational technology for industrial processes | Legacy protocols, lack of patching capability, safety-over-security design |

---

## 3.2 Securing Enterprise Infrastructure
*Given a scenario, apply security principles to secure enterprise infrastructure.*

### Security Zones

| Zone | Trust Level | Typical Contents |
|------|-------------|-----------------|
| **Internet (External)** | Untrusted | Public DNS, CDN edge nodes |
| **DMZ (Demilitarized Zone)** | Semi-trusted (screened subnet) | Public web servers, email relays, external-facing APIs |
| **Internal** | Trusted | Employee workstations, internal application servers |
| **Restricted** | Highly trusted | HR systems, financial data, PII/PHI, domain controllers |

**DMZ architecture:** Positioned between two firewalls (or between the external firewall and the internet). Systems in the DMZ are accessible from the internet but cannot directly access the internal network.

### Network Appliances — Types and Placement

| Appliance | Function | Placement |
|-----------|----------|-----------|
| **Firewall (Stateful)** | Filters traffic based on connection state and rules | Network perimeter; between zones |
| **WAF** | Inspects HTTP/S; blocks application-layer attacks (SQLi, XSS, CSRF) | In front of public web applications |
| **UTM** | All-in-one: firewall + IDS/IPS + antivirus + DLP + content filtering | SMB environments; single-appliance deployments |
| **NGFW** | Stateful firewall + Layer 7 application identification + IPS + TLS inspection | Enterprise perimeters; replaces traditional firewalls |
| **IDS** | Passive detection; generates alerts; does NOT block traffic | Out-of-band (receives copy of traffic via TAP or SPAN port) |
| **IPS** | Active; blocks malicious traffic in real-time | Inline (sits in the traffic path) |
| **Proxy Server** | Intermediary for client requests; can enforce policy and provide anonymity | Forward proxy (internal clients → internet); Reverse proxy (internet → internal servers) |
| **Jump Server (Bastion Host)** | Hardened, audited gateway for administrative access to secure network zones | Between management workstations and secured segments |
| **Load Balancer** | Distributes traffic across multiple servers for availability and performance | In front of server farms; Layer 4 (TCP/UDP) or Layer 7 (HTTP/S) |
| **CASB** | Enforces security policy between users and cloud applications | Between users and cloud SaaS/IaaS access |

### Device Attributes

| Attribute | Active / Inline | Passive / Out-of-Band |
|-----------|----------------|----------------------|
| **Traffic handling** | Sits in path; processes live traffic | Receives a copy of traffic (TAP/SPAN); does not affect flow |
| **Can block threats** | Yes | No — alerts only |
| **Examples** | IPS, firewall, WAF | IDS, packet capture, protocol analyzer |
| **Failure modes** | **Fail-open** (traffic passes on failure) or **Fail-closed** (traffic blocked on failure) | Failure does not affect traffic flow |

> **Exam Tip — Fail-open vs. Fail-closed:** Choose based on priority:
> - **Fail-closed** → prioritizes **security** over availability (traffic blocked if device fails)
> - **Fail-open** → prioritizes **availability** over security (traffic passes if device fails)
> A security-critical device protecting sensitive data should be **fail-closed**.

### Secure Communication Protocols

| Protocol | OSI Layer | Use Case |
|----------|-----------|---------|
| **TLS 1.2 / 1.3** | 4–7 | HTTPS, SMTPS, IMAPS, FTPS — encrypts data in transit |
| **IPsec** | 3 | VPNs; Tunnel mode (encrypts full packet) vs. Transport mode (encrypts payload only) |
| **SSH** | 7 | Encrypted remote administration; replaces cleartext Telnet |
| **SRTP** | 7 | Encrypted VoIP / real-time media |
| **DNSSEC** | 7 | DNS integrity verification via digital signatures; does not encrypt DNS, only authenticates |

### Secure Access Service Edge (SASE)
SASE converges SD-WAN capabilities with cloud-native security functions — including CASB, Secure Web Gateway (SWG), Zero Trust Network Access (ZTNA), and Firewall-as-a-Service (FWaaS) — into a single, cloud-delivered service model. Designed for distributed workforces and cloud-first environments where users access resources outside the traditional perimeter.

---

## 3.3 Protecting Data
*Compare and contrast concepts and strategies to protect data.*

### Data Classifications

| Classification | Sensitivity | Examples |
|---------------|-------------|---------|
| **Public** | No harm if disclosed | Marketing materials, press releases, public website content |
| **Internal / Private** | Moderate harm if disclosed | Employee directories, internal memos, project roadmaps |
| **Confidential / Sensitive** | Significant harm if disclosed | Business strategies, source code, contracts, customer data |
| **Restricted / Secret / Critical** | Severe harm if disclosed | PII, PHI, credentials, cryptographic keys, financial records |

### Data States and Protection Methods

| State | Definition | Primary Protection Methods |
|-------|------------|---------------------------|
| **Data at Rest** | Stored data (disk, tape, database, USB) | Full disk encryption (FDE), file/folder encryption, database encryption, access control |
| **Data in Transit** | Moving across a network or communication channel | TLS, IPsec, VPN, SFTP, HTTPS, SRTP |
| **Data in Use** | Being actively processed (in RAM or CPU cache) | Trusted Execution Environments (TEE), memory encryption, secure enclaves |

### Data Security Techniques

| Technique | How It Works | Primary Use Case |
|-----------|-------------|-----------------|
| **Encryption** | Transforms data into unreadable ciphertext using a key | Confidentiality — at rest and in transit |
| **Hashing** | One-way fixed-length digest of data | Integrity — detecting unauthorized modification |
| **Data Masking** | Replaces sensitive data with realistic but fictional substitute data | Non-production environments (development, testing, QA) |
| **Tokenization** | Replaces sensitive data with a randomly generated, meaningless token | Production systems — reduces PCI DSS scope for payment data |
| **Obfuscation** | Makes data or code difficult to read or interpret | Software protection; not a true confidentiality control |
| **Steganography** | Hides secret data within non-secret carrier media (image, audio) | Covert communication; also used by attackers for exfiltration |
| **Digital Rights Management (DRM)** | Controls how digital content can be accessed, copied, or distributed | Intellectual property and media content protection |

> **Exam Tip — Masking vs. Tokenization:**
> - **Masking** → fake-but-realistic data (e.g., "John Smith" becomes "Jane Doe") → used in **non-production** (dev/test environments)
> - **Tokenization** → meaningless placeholder that maps to real data in a secure vault → used in **production** (reduces PCI DSS scope)
> Both remove sensitive data from the environment, but tokenization is reversible by the vault; masking typically is not.

---

## 3.4 Resilience and Recovery
*Explain the importance of resilience and recovery in security architecture.*

### Recovery Site Types

| Site Type | Hardware | Data | Recovery Time | Cost |
|-----------|----------|------|---------------|------|
| **Hot Site** | Present and running | Continuously synced | Minutes to hours | Highest |
| **Warm Site** | Present but not fully configured | Partially current; needs recent backup | Hours to days | Medium |
| **Cold Site** | Not present (empty facility with power/HVAC/connectivity) | Not present | Days to weeks | Lowest |
| **Mobile Site** | Self-contained portable unit | Depends on configuration | Variable | Variable |
| **Cloud-Based DR** | Provisioned on demand | Replicated from primary | Minutes (pre-configured) | Pay-as-you-go |

### High Availability Concepts

| Concept | Definition |
|---------|------------|
| **High Availability (HA)** | Design principle ensuring a system remains operational for the maximum possible percentage of time |
| **Load Balancing** | Distributes incoming traffic across multiple servers; provides HA and improves performance |
| **Clustering** | Multiple servers act as a single logical system; automatic failover if a node fails |
| **Geographic Dispersion** | Systems distributed across multiple physical locations; protects against regional disasters |
| **Platform Diversity** | Using different OS types or vendors to prevent a single vulnerability from taking down all systems |
| **Continuity of Operations (COOP)** | Plans and procedures to ensure critical functions continue during a disruption |

### Backup Types

| Backup Type | What It Captures | Restore Process | Storage Need |
|------------|------------------|-----------------|-------------|
| **Full** | All selected data every time | Single set — fastest | Most |
| **Incremental** | Changes since last backup (full or incremental) | Requires full + all incrementals — slowest | Least |
| **Differential** | Changes since last full backup | Requires full + latest differential — medium | Medium |
| **Snapshot** | Point-in-time image of a system or volume (common in VMs) | Near-instant restore | Variable |

**Best practice:** Implement the **3-2-1 rule** — 3 copies of data, on 2 different media types, with 1 copy stored offsite.

### Key Recovery Metrics

| Metric | Definition | Key Question |
|--------|------------|-------------|
| **RTO** (Recovery Time Objective) | Maximum acceptable time to restore a service after a disruption | "How fast must we recover?" |
| **RPO** (Recovery Point Objective) | Maximum acceptable amount of data loss measured in time | "How old can restored data be?" |
| **MTBF** (Mean Time Between Failures) | Average time a system operates before experiencing a failure | "How reliable is this system?" |
| **MTTR** (Mean Time to Repair) | Average time required to restore a failed system to operation | "How quickly can we fix it?" |

> **Exam Tip — RTO vs. RPO:**
> - **RTO** is about **downtime** — the maximum acceptable duration without service
> - **RPO** is about **data loss** — the maximum acceptable age of recovered data
> - A 4-hour RPO means backups must run at least every 4 hours; a disaster at hour 3.5 results in ≤4 hours of data loss

### DR / BCP Testing Methods

| Test Type | Description | Operational Disruption |
|-----------|-------------|----------------------|
| **Tabletop Exercise** | Discussion-based walkthrough; team talks through a scenario | None |
| **Walk-Through / Read-Through** | Plans reviewed for accuracy and completeness | None |
| **Simulation** | Mimics a disaster scenario without actual failover | Low |
| **Parallel Test** | Alternate site activated while primary remains in operation | Low |
| **Full Interruption** | Primary site shut down; full cutover to alternate site | High — tests real-world recovery |

---

## Study Checklist

### 3.1 Architecture Models
- [ ] Compare public, private, hybrid, and multi-cloud deployment models and their specific security considerations
- [ ] Explain the shared responsibility model and identify the boundary between CSP and customer responsibilities
- [ ] Describe containerization vs. virtualization: different isolation levels and respective security risks
- [ ] Explain what IaC is, and how version control and peer review apply to infrastructure changes
- [ ] Define air-gapped networks and explain when they are appropriate

### 3.2 Securing Enterprise Infrastructure
- [ ] Correctly place a DMZ in a network architecture diagram
- [ ] Distinguish WAF, UTM, NGFW, IDS, and IPS — know what each does and its correct placement
- [ ] Explain fail-open vs. fail-closed and select the appropriate mode for a given security requirement
- [ ] Describe the role of a jump server and why it must be hardened
- [ ] Compare TLS, IPsec (Tunnel vs. Transport mode), and SSH for securing data in transit
- [ ] Explain SASE and the use cases it addresses

### 3.3 Protecting Data
- [ ] Classify data by state (at rest, in transit, in use) and match to the appropriate protection method
- [ ] Distinguish data masking (non-production, fake data) from tokenization (production, reversible via vault)
- [ ] Explain DRM and identify scenarios where it is the appropriate control

### 3.4 Resilience and Recovery
- [ ] Compare hot, warm, and cold sites across readiness, recovery time, and cost
- [ ] Distinguish full, incremental, and differential backups in terms of restore speed and storage trade-offs
- [ ] Define RTO and RPO and explain the difference with a concrete example
- [ ] Recall the 3-2-1 backup rule
- [ ] List the five DR testing methods in order of operational disruption
- [ ] Explain geographic dispersion and platform diversity as resilience strategies
