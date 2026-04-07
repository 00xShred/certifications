# SY0-701 Must-Know Ports and Protocols
**Final Prep Reference**

Know these cold. Port numbers appear in firewall rule questions, log analysis scenarios, and network configuration PBQs (performance-based questions).

---

## Well-Known Ports (0–1023)

| Port(s) | Protocol | Service | Key Details |
|---------|----------|---------|-------------|
| **20** | TCP | FTP (Data) | Active mode: server initiates data connection from port 20 |
| **21** | TCP | FTP (Control) | Commands and authentication; cleartext — replace with SFTP or FTPS |
| **22** | TCP | SSH / SFTP / SCP | Encrypted remote shell; SFTP and SCP also run on port 22 |
| **23** | TCP | Telnet | Unencrypted remote login — **do not use**; replace with SSH |
| **25** | TCP | SMTP | Mail transfer between servers; often blocked outbound to prevent spam relay |
| **53** | TCP/UDP | DNS | UDP for queries; TCP for zone transfers and responses >512 bytes |
| **67** | UDP | DHCP (Server) | Server listens for DHCP discover broadcasts |
| **68** | UDP | DHCP (Client) | Client receives IP lease offer from DHCP server |
| **69** | UDP | TFTP | No authentication; used for network booting and firmware delivery |
| **80** | TCP | HTTP | Unencrypted web traffic — replace with HTTPS |
| **110** | TCP | POP3 | Retrieve email; downloads and typically deletes from server |
| **123** | UDP | NTP | Network time sync — critical for Kerberos (5-min clock skew limit) and log correlation |
| **143** | TCP | IMAP | Retrieve and sync email; messages remain on server |
| **161** | UDP | SNMP (Query) | Network device monitoring and management |
| **162** | UDP | SNMP (Trap) | Unsolicited alert sent from a device to a management station |
| **389** | TCP | LDAP | Directory services (AD lookups); cleartext — replace with LDAPS |
| **443** | TCP | HTTPS | HTTP over TLS — standard secure web |
| **445** | TCP | SMB / CIFS | Windows file sharing; was exploited by WannaCry/EternalBlue — restrict aggressively |
| **514** | UDP | Syslog | Log forwarding; use TCP/TLS (port 6514) for secure transport |
| **636** | TCP | LDAPS | LDAP over TLS — encrypted directory queries |
| **993** | TCP | IMAPS | IMAP over TLS |
| **995** | TCP | POP3S | POP3 over TLS |

---

## Registered Ports (1024–49151)

| Port(s) | Protocol | Service | Key Details |
|---------|----------|---------|-------------|
| **1433** | TCP | Microsoft SQL Server | Restrict access; never expose to the internet |
| **1812** | UDP | RADIUS (Authentication) | AAA for network access control (Wi-Fi, VPN) |
| **1813** | UDP | RADIUS (Accounting) | Session usage and accounting records |
| **3306** | TCP | MySQL | Default MySQL/MariaDB port — restrict access |
| **3389** | TCP | RDP | Remote Desktop Protocol — high-value attack target; restrict to VPN/jump server access only |
| **5060** | TCP/UDP | SIP | VoIP signaling — unencrypted |
| **5061** | TCP | SIPS | SIP over TLS — encrypted VoIP signaling |
| **8080** | TCP | HTTP Alternate | Common alternate web/proxy port |
| **8443** | TCP | HTTPS Alternate | Common alternate HTTPS port |

---

## Protocol Quick Reference

| Protocol | Layer | Port / Number | Purpose |
|----------|-------|--------------|---------|
| **ICMP** | 3 | — (IP Protocol 1) | Ping, traceroute, error reporting |
| **ARP** | 2 | — | IP to MAC address resolution |
| **Kerberos** | 7 | TCP/UDP 88 | Default authentication for Active Directory |
| **IPsec ESP** | 3 | IP Protocol 50 | VPN encryption |
| **IPsec AH** | 3 | IP Protocol 51 | VPN authentication / integrity (no encryption) |
| **GRE** | 3 | IP Protocol 47 | Generic tunnel encapsulation |

---

## Secure vs. Insecure Protocol Pairs

| Insecure Protocol | Port | Secure Replacement | Port |
|-------------------|------|--------------------|------|
| HTTP | 80 | HTTPS (HTTP + TLS) | 443 |
| Telnet | 23 | SSH | 22 |
| FTP | 20/21 | SFTP (via SSH) | 22 |
| FTP | 20/21 | FTPS (FTP + TLS) | 990 |
| LDAP | 389 | LDAPS (LDAP + TLS) | 636 |
| IMAP | 143 | IMAPS | 993 |
| POP3 | 110 | POP3S | 995 |
| SMTP | 25 | SMTPS (STARTTLS) | 587 / 465 |
| SNMPv1/v2c | 161 | SNMPv3 | 161 |
| Syslog (UDP) | 514 | Syslog over TLS | 6514 |

---

## Exam Tips

- **Port 22 carries SSH, SFTP, and SCP** — all three use the same port
- **DNS uses both UDP and TCP** — UDP for queries, TCP for zone transfers
- **SNMP v1/v2c** transmit community strings in cleartext — SNMPv3 adds authentication and encryption
- **RDP (3389)** is a top attack target and should never be exposed directly to the internet; require VPN or jump server access
- **SMB (445)** was the attack vector for WannaCry and EternalBlue — always block at the network perimeter
- **NTP (123)** is security-critical: Kerberos authentication fails if clocks are off by more than 5 minutes; NTP can also be abused for DDoS amplification attacks
- **RADIUS uses two ports**: 1812 for authentication, 1813 for accounting
