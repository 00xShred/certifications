# SY0-701 CLI Tools Reference
**Final Prep Reference**

These command-line tools appear in PBQ (performance-based question) scenarios and in network troubleshooting and forensics questions. Know the tool's purpose, its key flags, and how to interpret its output.

---

## `ping`

**Purpose:** Tests network connectivity and latency using ICMP Echo Request/Reply.

```bash
ping 8.8.8.8
```

**Sample output:**
```
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=12.4 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=11.9 ms
```

**Key flags:**
| Flag | Function |
|------|----------|
| `-c 4` (Linux) / `-n 4` (Windows) | Send a specific number of packets |
| `-t` (Windows) | Ping continuously until stopped |

**Exam relevance:** Connectivity testing; ICMP blocking by firewalls means no response does not always indicate a host is down.

---

## `ipconfig` / `ifconfig` / `ip`

**Purpose:** Displays and configures network interface settings (IP address, subnet mask, gateway, DNS).

```bash
ipconfig /all          # Windows — full detail including DNS servers and MAC
ifconfig -a            # Linux (legacy)
ip addr show           # Linux (modern)
```

**Sample output (ipconfig /all):**
```
IPv4 Address. . . . . . : 192.168.1.10
Subnet Mask . . . . . . : 255.255.255.0
Default Gateway . . . . : 192.168.1.1
DNS Servers . . . . . . : 8.8.8.8
```

**Exam relevance:** Identify IP configuration issues; verify DNS server assignments; `/release` and `/renew` for DHCP troubleshooting; `/flushdns` clears the local DNS cache.

---

## `nslookup` / `dig`

**Purpose:** Query DNS servers to resolve names and troubleshoot DNS issues. `dig` provides more granular output.

```bash
nslookup example.com
dig example.com
dig @8.8.8.8 example.com MX    # Query specific DNS server for MX records
```

**Sample output (dig):**
```
;; ANSWER SECTION:
example.com.   300   IN   A   93.184.216.34

;; Query time: 23 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
```

**Exam relevance:** DNS poisoning investigation; verify correct record resolution; identify unauthorized DNS changes; MX records for email security (SPF, DKIM).

---

## `netstat`

**Purpose:** Displays active network connections, listening ports, routing tables, and interface statistics.

```bash
netstat -ano        # Windows: all connections, numeric, with PID
netstat -tulnp      # Linux: TCP/UDP listening ports with PID
```

**Sample output (`netstat -ano`):**
```
Proto  Local Address      Foreign Address    State        PID
TCP    0.0.0.0:445        0.0.0.0:0          LISTENING    4
TCP    192.168.1.10:50123 142.250.80.1:443   ESTABLISHED  1234
```

**Key flags:**
| Flag | Function |
|------|----------|
| `-a` | Show all connections (listening + established) |
| `-n` | Show numeric addresses (no hostname resolution) |
| `-o` / `-p` | Show the PID / process name associated with each connection |

**Exam relevance:** Identify unexpected listening ports (backdoors, malware); trace which process owns a suspicious connection; detect unauthorized services.

---

## `tracert` (Windows) / `traceroute` (Linux)

**Purpose:** Displays the hop-by-hop path a packet takes to reach a destination, with latency per hop.

```bash
tracert 8.8.8.8          # Windows
traceroute 8.8.8.8       # Linux
```

**Sample output:**
```
 1    <1 ms   <1 ms   <1 ms  192.168.1.1
 2     2 ms    2 ms    2 ms  10.0.0.1
 3    12 ms   11 ms   12 ms  8.8.8.8
```

**Exam relevance:** Identify where in the network path connectivity fails; detect routing anomalies; `* * *` indicates ICMP is blocked at that hop (not necessarily a failure).

---

## `nmap`

**Purpose:** Network discovery and security auditing — port scanning, service/version detection, OS fingerprinting.

```bash
nmap -sS -p 1-1000 192.168.1.1       # TCP SYN (stealth) scan of ports 1–1000
nmap -sV -O 192.168.1.0/24           # Version and OS detection across a subnet
nmap -sU -p 53,161 192.168.1.1       # UDP scan for DNS and SNMP
```

**Sample output:**
```
PORT     STATE  SERVICE  VERSION
22/tcp   open   ssh      OpenSSH 8.9
80/tcp   open   http     Apache 2.4.52
443/tcp  open   https    Apache 2.4.52
3389/tcp open   rdp
```

**Key scan types:**
| Flag | Scan Type | Notes |
|------|-----------|-------|
| `-sS` | TCP SYN (stealth) | Does not complete handshake; less likely to be logged |
| `-sT` | TCP Connect | Full handshake; more detectable |
| `-sU` | UDP scan | Slower; needed to find SNMP, DNS, DHCP |
| `-sV` | Service version | Identifies the application and version running |
| `-O` | OS detection | Requires root/admin; uses TTL and TCP window fingerprinting |

**Exam relevance:** Vulnerability management; attack surface enumeration; used in both offensive (reconnaissance) and defensive (asset discovery) contexts. Requires authorization before use.

---

## `tcpdump`

**Purpose:** Command-line packet capture and analysis tool. Captures live network traffic or reads existing capture files.

```bash
tcpdump -i eth0                          # Capture all traffic on eth0
tcpdump -i eth0 -w capture.pcap          # Write to file for later analysis
tcpdump -i eth0 host 192.168.1.10        # Filter traffic to/from specific IP
tcpdump -i eth0 port 443                 # Filter by port
tcpdump -r capture.pcap                  # Read from capture file
```

**Sample output:**
```
12:01:05.123 IP 192.168.1.10.50123 > 8.8.8.8.443: Flags [S], seq 12345678, win 65535
12:01:05.135 IP 8.8.8.8.443 > 192.168.1.10.50123: Flags [S.], seq 87654321, ack 12345679
```

**Exam relevance:** Forensic packet analysis; detecting cleartext credentials; identifying beaconing patterns; capturing evidence during an active incident.

---

## `arp`

**Purpose:** Displays and manages the ARP (Address Resolution Protocol) cache — IP to MAC address mappings.

```bash
arp -a        # Display the full ARP cache (Windows and Linux)
arp -d        # Delete an ARP entry
```

**Sample output:**
```
Internet Address    Physical Address    Type
192.168.1.1         00-11-22-33-44-55   dynamic
192.168.1.25        66-77-88-99-aa-bb   dynamic
```

**Exam relevance:** **ARP poisoning / ARP spoofing** detection — look for duplicate MAC addresses for different IPs, or a gateway IP mapping to an unexpected MAC. Dynamic ARP Inspection (DAI) on managed switches mitigates this.

---

## `route`

**Purpose:** Displays and modifies the IP routing table.

```bash
route print           # Windows
ip route show         # Linux (modern)
netstat -r            # Both platforms
```

**Sample output (Windows):**
```
Network Destination    Netmask         Gateway        Interface    Metric
0.0.0.0                0.0.0.0         192.168.1.1    192.168.1.10  25
192.168.1.0            255.255.255.0   On-link        192.168.1.10  281
```

**Exam relevance:** Verify default gateway configuration; detect unauthorized static routes that could redirect traffic (a route injection attack).

---

## Quick Reference: Tool → Use Case

| Tool | Primary Security Use Case |
|------|--------------------------|
| `ping` | Connectivity testing; ICMP reachability |
| `ipconfig`/`ip` | Interface configuration; DNS verification |
| `nslookup`/`dig` | DNS resolution; detect DNS poisoning |
| `netstat` | Find unexpected open ports or active connections |
| `tracert`/`traceroute` | Path analysis; detect routing anomalies |
| `nmap` | Port and service discovery; vulnerability enumeration |
| `tcpdump` | Packet capture; forensic traffic analysis |
| `arp` | ARP cache inspection; detect ARP poisoning |
| `route` | Routing table inspection; detect route injection |
