# IPv4 Addressing and Packet Structure

## What is an IP Address?

**IP (Internet Protocol)** is a protocol used for addressing and routing data packets across networks.

An **IP address** is a logical numerical address assigned to a network interface, allowing devices to communicate with each other over IP networks such as local networks and the Internet.

### Example IPv4 Address

```text
192.168.120.102
```

---

## Why Do IP Addresses Exist?

IP addresses serve two primary purposes:

### 1. Identification

They uniquely identify a device or network interface on a network.

### 2. Routing (Location Addressing)

They indicate where a device is located within a network hierarchy, allowing routers to forward packets to the correct destination.

---

# IP Versions

There are two major versions of the Internet Protocol currently in use:

| Version | Description                 |
| ------- | --------------------------- |
| IPv4    | Internet Protocol Version 4 |
| IPv6    | Internet Protocol Version 6 |

This document focuses on **IPv4**.

---

# IPv4 Structure

An IPv4 address consists of **32 bits** divided into **four octets** (bytes).

### Example

```text
192.168.120.102
```

Binary representation:

```text
11000000.10101000.01111000.01100110
```

---

## Octets

An IPv4 address contains four sections separated by dots (`.`).

```text
192.168.120.102
```

| Octet        | Value |
| ------------ | ----- |
| First Octet  | 192   |
| Second Octet | 168   |
| Third Octet  | 120   |
| Fourth Octet | 102   |

Each octet contains:

```text
1 Octet = 8 Bits = 1 Byte
```

### Value Range of an Octet

Since 8 bits can represent 256 possible values:

```text
00000000 = 0
11111111 = 255
```

Therefore:

```text
Range: 0 - 255
```

---

## Dotted Decimal Notation

Humans typically read IPv4 addresses in decimal form:

```text
192.168.120.102
```

Computers process the address in binary form:

```text
11000000.10101000.01111000.01100110
```

This decimal representation is called:

```text
Dotted Decimal Notation
```

---

# Binary Representation Example

IPv4 addresses are stored and processed as binary values.

Example:

```text
185.107.80.231
```

Convert each octet to binary:

```text
185 = 10111001
107 = 01101011
80  = 01010000
231 = 11100111
```

Result:

```text
10111001.01101011.01010000.11100111
```

---

# Network and Host Portions

Every IPv4 address consists of two logical parts:

## Network Portion

Identifies the network to which the device belongs.

## Host Portion

Identifies the specific device within that network.

### Example

```text
192.168.1.50/24
```

Network Portion:

```text
192.168.1
```

Host Portion:

```text
50
```

The division between network and host portions is determined by the subnet mask or CIDR prefix.

---

# Types of IPv4 Addresses

## 1. Unicast

Communication from one sender to one receiver.

```text
1 → 1
```

Example:

```text
Your PC communicating with a web server.
```

---

## 2. Broadcast

Communication from one sender to all hosts on a network.

```text
1 → All
```

Example:

```text
192.168.1.255
```

---

## 3. Multicast

Communication from one sender to a selected group of receivers.

```text
1 → Many
```

Commonly used for:

* Streaming
* Routing protocols
* Video conferencing

---

# IPv4 Packet Structure

When data is transmitted across an IP network, it is encapsulated into an IPv4 packet.

An IPv4 packet consists of:

```text
+----------------+
| IPv4 Header    |
+----------------+
| Payload (Data) |
+----------------+
```

---

## Maximum Packet Size

The IPv4 Total Length field is 16 bits.

Maximum packet size:

```text
2^16 - 1 = 65535 bytes
```

---

## MTU (Maximum Transmission Unit)

MTU is the largest packet size that can be transmitted over a network link without fragmentation.

### Standard Ethernet MTU

```text
1500 bytes
```

Typical packet:

```text
20-byte IPv4 Header
1480-byte Payload
```

---

## IPv4 Header Size

| Header Type    | Size     |
| -------------- | -------- |
| Minimum Header | 20 Bytes |
| Maximum Header | 60 Bytes |

The header can grow when optional fields are included.

---

# IPv4 Header Fields

## Version

Specifies the IP version being used.

| Value | Version |
| ----- | ------- |
| 4     | IPv4    |
| 6     | IPv6    |

Field size:

```text
4 Bits
```

---

## Internet Header Length (IHL)

Indicates the size of the IPv4 header.

Formula:

```text
IHL × 4 Bytes
```

Examples:

```text
5 × 4 = 20 Bytes
15 × 4 = 60 Bytes
```

---

## Type of Service (ToS)

Indicates how routers should handle packet priority and quality of service.

Modern implementations use:

* DSCP
* ECN

---

## Total Length

Specifies the total size of the packet.

Includes:

```text
Header + Payload
```

Maximum:

```text
65535 Bytes
```

---

## Identification

A unique identifier used during fragmentation.

All fragments of the same original packet share the same Identification value.

Field size:

```text
16 Bits
```

---

## Flags

Controls packet fragmentation.

Contains three flags:

| Flag     | Purpose        |
| -------- | -------------- |
| Reserved | Must be 0      |
| DF       | Don't Fragment |
| MF       | More Fragments |

---

## Fragment Offset

Indicates the position of a fragment within the original packet.

Used during packet reassembly.

---

## TTL (Time To Live)

Limits the lifetime of a packet.

Every router that forwards a packet decreases the TTL value by 1.

When TTL reaches:

```text
0
```

The packet is discarded.

This mechanism prevents routing loops.

Field size:

```text
8 Bits
```

---

## Protocol

Identifies the protocol encapsulated within the IPv4 payload.

Examples:

| Protocol | Number |
| -------- | ------ |
| ICMP     | 1      |
| TCP      | 6      |
| UDP      | 17     |
| OSPF     | 89     |

---

## Header Checksum

Used to detect errors in the IPv4 header.

Important:

```text
Checks only the Header
```

It does not verify payload data.

Field size:

```text
16 Bits
```

---

## Source Address

The IPv4 address of the sender.

Field size:

```text
32 Bits
```

---

## Destination Address

The IPv4 address of the receiver.

Field size:

```text
32 Bits
```

---

# Important IPv4 Concepts

## Private Address Ranges

| Range                         | CIDR           |
| ----------------------------- | -------------- |
| 10.0.0.0 - 10.255.255.255     | 10.0.0.0/8     |
| 172.16.0.0 - 172.31.255.255   | 172.16.0.0/12  |
| 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 |

---

## Loopback Address

Used for testing the local network stack.

```text
127.0.0.1
```

Hostname:

```text
localhost
```

---

## APIPA

Automatic Private IP Addressing.

Used when a device cannot obtain an address from DHCP.

Range:

```text
169.254.0.0/16
```

---

## CIDR Notation

CIDR specifies how many bits belong to the network portion.

Examples:

```text
/8
/16
/24
/30
```

Example:

```text
192.168.1.0/24
```

---

## Subnet Masks

Common subnet masks:

| CIDR | Subnet Mask   |
| ---- | ------------- |
| /8   | 255.0.0.0     |
| /16  | 255.255.0.0   |
| /24  | 255.255.255.0 |

---

## NAT (Network Address Translation)

NAT allows multiple private IP addresses to share a single public IP address.

Benefits:

* Conserves IPv4 addresses
* Hides internal network structure
* Commonly used in home and enterprise networks
