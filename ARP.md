# Address Resolution Protocol (ARP)
## 1. What is ARP?

ARP (Address Resolution Protocol) is a Layer 2 protocol used in IPv4 networks to map an IP address (Layer 3) to a MAC address (Layer 2) within a Local Area Network (LAN).

Without ARP, devices would not know the MAC address of the destination host, and communication inside a LAN would fail.

> ARP is only used in IPv4. IPv6 uses Neighbor Discovery Protocol (NDP) instead.

## 2. Why ARP is Needed

When a device wants to send data inside a local network:

- It knows the destination IP

- It does NOT know the destination MAC

- Ethernet frames require a destination MAC address

- Therefore → ARP is used to resolve IP → MAC

## 3. How ARP Works (Step-by-Step)

Scenario:

Host A wants to send data to Host B in the same network.

## Step 1 — ARP Request (Broadcast)

- Host A checks its ARP cache

- If no entry exists, it sends an ARP Request

- The request is broadcast to the entire LAN

- Destination MAC:
```
  FF:FF:FF:FF:FF:FF
```

- Message format:
```
  Who has 192.168.1.10?
  Tell 192.168.1.5
```

> All devices receive this frame.

## Step 2 — ARP Reply (Unicast)

- Only Host B (the owner of 192.168.1.10) responds

- The reply is sent directly (unicast) to Host A

- Message format:
```
  192.168.1.10 is at 00:1A:2B:3C:4D:5E
```
## Step 3 — ARP Table Update

- Host A stores the mapping in its ARP cache

- Switch learns MAC addresses from frames

- Communication starts

## 4. ARP Packet Structure

An ARP packet contains:

 ```
 Hardware Type	Ethernet = 1
 Protocol Type	IPv4 = 0x0800
 Hardware Size	MAC length (6 bytes)
 Protocol Size	IPv4 length (4 bytes)
 Opcode	1 = Request, 2 = Reply
 Sender MAC	MAC of sender
 Sender IP	IP of sender
 Target MAC	Unknown in request (00:00:00:00:00:00)
Target IP	IP being resolved
```

## 5. ARP Cache

Each device maintains an ARP table.

View ARP table:

- Linux:

```bash
arp -a
```

**or**

```bash
ip neigh
```

- Windows:

```powershell
arp -a
```

Entries are temporary and expire after some time.

## 6. Types of ARP

#### 1. Standard ARP

Normal ARP request and reply process.

#### 2. Gratuitous ARP

A device sends ARP for its own IP.
Used to:

- Detect IP conflicts

- Update ARP tables

- High availability systems

#### 3. Proxy ARP

A router responds to ARP on behalf of another host.

## 7. ARP and the Switch

Important clarification:

- ARP request is broadcast

- Switch floods broadcast frames

- ARP reply is unicast

- Switch learns MAC addresses from source fields

- ARP itself does NOT make the switch learn MAC addresses.
  The switch learns MAC addresses from any incoming frame.

## 8. ARP Security Issues

- ARP Spoofing / ARP Poisoning

- An attacker sends fake ARP replies to:

- Associate attacker MAC with victim IP

- Perform Man-in-the-Middle attack

- Intercept or modify traffic

**Example attack flow:**

```Attacker tells victim: "Router IP is my MAC"

Attacker tells router: "Victim IP is my MAC"

Traffic flows through attacker
```
## 9. ARP Limitations

- Works only inside a LAN

- Not routable

- No authentication

- Vulnerable to spoofing

- Only for IPv4

---

## 10. Quick Summary

- ARP maps IP → MAC

- Used inside LAN

- Request = Broadcast

- Reply = Unicast

- Cached temporarily

- Vulnerable to spoofing
