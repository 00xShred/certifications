# SY0-701 Must-Know Ports and Protocols

**Final Prep Reference**

Know these cold. Port numbers appear in firewall rule questions, log analysis scenarios, and network configuration PBQs (performance-based questions).

---

## Well-Known Ports (0–1023)

| Port(s)     | Protocol | Service              | Key Details                                                                            |
| ----------- | -------- | -------------------- | -------------------------------------------------------------------------------------- |
| **20**      | TCP      | FTP (Data)           | Active mode: server initiates data connection from port 20                             |
| **21**      | TCP      | FTP (Control)        | Commands and authentication; cleartext — replace with SFTP or FTPS                    |
| **22**      | TCP      | SSH / SFTP / SCP     | Encrypted remote shell; SFTP and SCP also run on port 22                               |
| **23**      | TCP      | Telnet               | Unencrypted remote login — **do not use**; replace with SSH                            |
| **25**      | TCP      | SMTP                 | Mail transfer between servers; often blocked outbound to prevent spam relay            |
| **49**      | TCP      | TACACS+              | Cisco-proprietary AAA; unlike RADIUS, encrypts the **entire** packet                  |
| **53**      | TCP/UDP  | DNS                  | UDP for queries; TCP for zone transfers and responses >512 bytes                       |
| **67**      | UDP      | DHCP (Server)        | Server listens for DHCP discover broadcasts                                            |
| **68**      | UDP      | DHCP (Client)        | Client receives IP lease offer from DHCP server                                        |
| **69**      | UDP      | TFTP                 | No authentication; used for network booting and firmware delivery                      |
| **80**      | TCP      | HTTP                 | Unencrypted web traffic — replace with HTTPS                                           |
| **88**      | TCP/UDP  | Kerberos             | Active Directory SSO; issues tickets via the Key Distribution Center (KDC)             |
| **110**     | TCP      | POP3                 | Retrieve email; downloads and typically deletes from server                            |
| **123**     | UDP      | NTP                  | Network time sync — critical for Kerberos (5-min clock skew limit) and log correlation |
| **137–139** | TCP/UDP  | NetBIOS              | Legacy Windows networking; often flagged in vulnerability scans of older systems       |
| **143**     | TCP      | IMAP                 | Retrieve and sync email; messages remain on server                                     |
| **161**     | UDP      | SNMP (Query)         | Network device monitoring and management                                               |
| **162**     | UDP      | SNMP (Trap)          | Unsolicited alert sent from a device to a management station                           |
| **389**     | TCP      | LDAP                 | Directory services (AD lookups); cleartext — replace with LDAPS                        |
| **443**     | TCP      | HTTPS                | HTTP over TLS — standard secure web                                                    |
| **445**     | TCP      | SMB / CIFS           | Windows file sharing; was exploited by WannaCry/EternalBlue — restrict aggressively    |
| **500**     | UDP      | ISAKMP / IKE         | Negotiates security associations for IPsec VPNs                                        |
| **502**     | TCP      | Modbus               | Common in ICS/SCADA environments; lacks native security/authentication                 |
| **514**     | UDP      | Syslog               | Log forwarding; use TCP/TLS (port 6514) for secure transport                           |
| **587**     | TCP      | SMTP Submission      | Modern secure method for clients to send mail using STARTTLS                           |
| **636**     | TCP      | LDAPS                | LDAP over TLS — encrypted directory queries                                            |
| **990**     | TCP      | FTPS (Implicit)      | FTP over TLS; encryption starts immediately upon connection                            |
| **993**     | TCP      | IMAPS                | IMAP over TLS                                                                          |
| **995**     | TCP      | POP3S                | POP3 over TLS                                                                          |

---

## Registered Ports (1024–49151)

| Port(s)         | Protocol | Service                 | Key Details                                                                                 |
| --------------- | -------- | ----------------------- | ------------------------------------------------------------------------------------------- |
| **1433**        | TCP      | Microsoft SQL Server    | Restrict access; never expose to the internet                                               |
| **1701**        | UDP      | L2TP                    | Layer 2 Tunneling Protocol; lacks encryption on its own — pair with IPsec                   |
| **1812**        | UDP      | RADIUS (Authentication) | AAA for network access control (Wi-Fi, VPN)                                                 |
| **1813**        | UDP      | RADIUS (Accounting)     | Session usage and accounting records                                                        |
| **1883**        | TCP      | MQTT                    | IoT messaging standard ("broker" model); cleartext — replace with MQTTS on 8883             |
| **3268**        | TCP      | LDAP Global Catalog     | Active Directory global catalog queries; cleartext                                          |
| **3269**        | TCP      | LDAPS Global Catalog    | LDAP Global Catalog over TLS                                                                |
| **3306**        | TCP      | MySQL                   | Default MySQL/MariaDB port — restrict access                                                |
| **3389**        | TCP      | RDP                     | Remote Desktop Protocol — high-value attack target; restrict to VPN/jump server access only |
| **4500**        | UDP      | IPsec NAT-T             | NAT Traversal; used when an IPsec VPN must pass through a NAT router                        |
| **5060**        | TCP/UDP  | SIP                     | VoIP signaling — unencrypted                                                                |
| **5061**        | TCP      | SIPS                    | SIP over TLS — encrypted VoIP signaling                                                     |
| **5683**        | UDP      | CoAP                    | Constrained Application Protocol; used for low-power IoT sensors                           |
| **6514**        | TCP      | Syslog over TLS         | Secure log forwarding to SIEM — always prefer over UDP 514                                  |
| **8080**        | TCP      | HTTP Alternate          | Common alternate web/proxy port                                                             |
| **8443**        | TCP      | HTTPS Alternate         | Common alternate HTTPS port                                                                 |
| **8883**        | TCP      | MQTTS                   | MQTT over TLS — encrypted IoT messaging                                                     |

---

## Protocol Quick Reference

| Protocol      | Layer | Port / Number     | Purpose                                        |
| ------------- | ----- | ----------------- | ---------------------------------------------- |
| **ICMP**      | 3     | — (IP Protocol 1) | Ping, traceroute, error reporting              |
| **ARP**       | 2     | —                 | IP to MAC address resolution                   |
| **Kerberos**  | 7     | TCP/UDP 88        | Default authentication for Active Directory    |
| **IPsec ESP** | 3     | IP Protocol 50    | VPN encryption                                 |
| **IPsec AH**  | 3     | IP Protocol 51    | VPN authentication / integrity (no encryption) |
| **GRE**       | 3     | IP Protocol 47    | Generic tunnel encapsulation                   |

---

## Secure vs. Insecure Protocol Pairs

| Insecure Protocol | Port      | Secure Replacement  | Port      |
| ----------------- | --------- | ------------------- | --------- |
| HTTP              | 80        | HTTPS (HTTP + TLS)  | 443       |
| Telnet            | 23        | SSH                 | 22        |
| FTP               | 20/21     | SFTP (via SSH)      | 22        |
| FTP               | 20/21     | FTPS (Explicit/TLS) | 990       |
| LDAP              | 389       | LDAPS (LDAP + TLS)  | 636       |
| LDAP GC           | 3268      | LDAPS GC            | 3269      |
| IMAP              | 143       | IMAPS               | 993       |
| POP3              | 110       | POP3S               | 995       |
| SMTP (Relay)      | 25        | SMTP (Submission)   | 587 / 465 |
| SNMPv1/v2c        | 161       | SNMPv3              | 161       |
| Syslog (UDP)      | 514       | Syslog over TLS     | 6514      |
| MQTT (IoT)        | 1883      | MQTTS               | 8883      |

---

## Exam Tips

- **Port 22 carries SSH, SFTP, and SCP** — all three use the same port
- **DNS uses both UDP and TCP** — UDP for queries, TCP for zone transfers
- **SNMP v1/v2c** transmit community strings in cleartext — SNMPv3 adds authentication and encryption
- **RDP (3389)** is a top attack target and should never be exposed directly to the internet; require VPN or jump server access
- **SMB (445)** was the attack vector for WannaCry and EternalBlue — always block at the network perimeter
- **NTP (123)** is security-critical: Kerberos authentication fails if clocks are off by more than 5 minutes; NTP can also be abused for DDoS amplification attacks
- **RADIUS uses two ports**: 1812 for authentication, 1813 for accounting
- **RADIUS vs. TACACS+**: RADIUS combines Authentication+Authorization and only encrypts the password; TACACS+ (port 49) separates all three AAA functions and encrypts the entire payload — used for device administration (e.g., managing routers)
- **Implicit vs. Explicit TLS**: Implicit (990, 993, 995) starts encrypted immediately; Explicit (587) starts as cleartext then upgrades via STARTTLS
- **NAT-T (4500)**: If a VPN fails because of PAT/NAT, ensure port 4500 is open for IPsec NAT Traversal
- **IoT protocols**: MQTT (1883) uses a broker model and is the most exam-likely IoT protocol; Modbus (502) appears in ICS/SCADA scenarios
- **Forwarding logs**: Always prefer **6514 (Syslog over TLS)** for SIEM transport to ensure confidentiality in transit
