# What Is a Network Protocol?

A network protocol is a formal set of rules that defines how devices communicate over a network. These rules specify how data is structured, addressed, transmitted, received, and interpreted so that different systems can understand each other reliably.

**Without network protocols:**

- Devices would not agree on data format

- Communication would fail even if a physical connection exists

- Networks would be unusable at scale

Protocols exist to solve specific communication problems at different layers of networking.

---

## Protocol Layers Overview

Network protocols are organized using models to separate responsibilities.

| Model        | Layers Involved                                     |
| ------------ | --------------------------------------------------- |
| OSI Model    | Layer 1 – Layer 7                                   |
| TCP/IP Model | Network Interface, Internet, Transport, Application |

**In practice, most protocols of interest to security professionals operate at:**

- Layer 2 (Data Link) – local communication

- Layer 3 (Network) – routing and addressing

- Layer 4 (Transport) – delivery mechanisms

- Layer 7 (Application) – user-facing services

---

## Layer 2 – Data Link Protocols
### ARP (Address Resolution Protocol)

ARP is used to translate a known IP address into a MAC address within a local network. When a device wants to communicate with another device on the same subnet, it must know the destination MAC address, and ARP provides this mapping.

ARP does not use ports and does not include authentication, because it assumes a trusted local network.

- Layer: OSI Layer 2

- Ports: None

- Scope: Local network only

**Security relevance:**
Because ARP blindly trusts replies, attackers can send fake ARP responses to associate their MAC address with another device’s IP. This enables ARP spoofing, which is commonly used in man-in-the-middle attacks to intercept or modify traffic.

---

## Layer 3 – Network Layer Protocols
### IP (Internet Protocol)

IP is responsible for logical addressing and packet routing across networks. It allows data to travel from a source device to a destination device, even if they are on different networks.

IP is a best-effort protocol, meaning it does not guarantee delivery, order, or reliability.

- Versions: IPv4, IPv6

- Layer: OSI Layer 3

- Ports: None (ports belong to Layer 4)

**Security relevance:**
IP is the foundation of all higher-level communication. Misconfigured routing, IP spoofing, and fragmentation abuse can all be leveraged during attacks.

### ICMP (Internet Control Message Protocol)

ICMP is used by devices to send error messages and operational information about network conditions. Tools like ping and traceroute rely on ICMP messages.

ICMP is encapsulated directly inside IP and does not use TCP or UDP.

- Layer: OSI Layer 3

- Ports: None

- IP Protocol Number: 1

**Security relevance:**
ICMP is heavily used for reconnaissance. Excessive ICMP traffic may indicate scanning or denial-of-service attempts. For this reason, many networks restrict or rate-limit ICMP.

---

## Layer 4 – Transport Layer Protocols
### TCP (Transmission Control Protocol)

TCP provides reliable, ordered, and error-checked data delivery. Before data transfer begins, TCP establishes a connection using a three-way handshake, ensuring both sides are ready to communicate.

Because reliability is prioritized over speed, TCP is used by applications where data integrity matters.

- Layer: OSI Layer 4

- Type: Connection-oriented

- Used by: HTTP, HTTPS, FTP, SSH, SMTP

**Security relevance:**
Attackers exploit TCP behavior using techniques such as SYN floods, session hijacking, and stealthy port scanning. SOC analysts frequently monitor TCP flags and connection patterns to detect anomalies.

### UDP (User Datagram Protocol)

UDP is a connectionless protocol designed for speed and low overhead. It sends data without establishing a session and does not guarantee delivery or order.

UDP is commonly used when performance matters more than reliability.

- Layer: OSI Layer 4

- Type: Connectionless

- Used by: DNS, DHCP, VoIP, streaming services

**Security relevance:**
UDP is widely abused in amplification attacks because it allows attackers to spoof source IP addresses. Its stateless nature also makes traffic harder to track and correlate.

---

## Application Layer Protocols
### DNS (Domain Name System)

DNS translates domain names into IP addresses, enabling users to access services without remembering numerical addresses. Most DNS queries use UDP for speed, while TCP is used for zone transfers and large responses.

- Ports: UDP 53 (queries), TCP 53 (zone transfers)

- Layer: Application

**Security relevance:**
DNS is frequently abused because it is almost always allowed through firewalls. Attackers use DNS tunneling to hide data exfiltration and command-and-control traffic inside DNS queries.

### HTTP (Hypertext Transfer Protocol)

HTTP is the protocol used for web communication. It transfers data in plaintext and does not provide encryption or authentication by default.

Port: TCP 80

State: Stateless

Layer: Application

Security relevance:
HTTP exposes sensitive data and is a common attack surface for web-based exploits. Any credentials or session tokens transmitted over HTTP can be intercepted.

HTTPS (HTTP Secure)

HTTPS is HTTP layered over TLS to provide encryption, integrity, and authentication. It is the standard protocol for modern web traffic.

Port: TCP 443

Layer: Application

Security relevance:
While HTTPS protects users, it also allows attackers to hide malicious traffic inside encrypted sessions. SOC teams rely on metadata, certificates, and traffic patterns for detection.

FTP (File Transfer Protocol)

FTP is a legacy protocol used for file transfer. It separates control and data channels and sends credentials in plaintext.

Ports: TCP 21 (control), TCP 20 (data)

Layer: Application

Security relevance:
FTP is insecure by design and should be avoided. Attackers often target FTP services for credential harvesting and unauthorized data access.

SSH (Secure Shell)

SSH provides secure remote access to systems using encryption. It supports both password-based and key-based authentication.

Port: TCP 22

Layer: Application

Security relevance:
SSH is frequently targeted by brute-force attacks. Compromised SSH access is a common method for persistence and lateral movement.

SMTP (Simple Mail Transfer Protocol)

SMTP is responsible for sending emails between servers and from clients to servers.

Ports: TCP 25 (server-to-server), TCP 587 (authenticated submission)

Layer: Application

Security relevance:
SMTP is a primary vector for phishing, spoofing, and malware delivery. Monitoring email flow is critical for SOC teams.

POP3 / IMAP

POP3 and IMAP are used by clients to retrieve emails from mail servers.

POP3: TCP 110

IMAP: TCP 143

Secure versions: POP3S (995), IMAPS (993)

Security relevance:
Unencrypted email retrieval exposes credentials. Secure variants should always be used.

DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP addresses and network configuration to devices joining a network.

Ports: UDP 67 (server), UDP 68 (client)

Layer: Application

Security relevance:
Attackers can deploy rogue DHCP servers to redirect traffic or perform man-in-the-middle attacks.

7. Secure vs Insecure Protocols
Insecure	Secure Alternative
HTTP	HTTPS
FTP	SFTP
Telnet	SSH
POP3	POP3S
IMAP	IMAPS
8. Why Protocol Knowledge Matters for Security Roles

SOC Analysts analyze protocol behavior to detect anomalies, malicious patterns, and policy violations.

Penetration Testers exploit weak protocols, misconfigurations, and insecure defaults to gain access and move laterally.

Understanding protocols at this level separates real practitioners from memorization-based learners.
