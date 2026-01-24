# Transmission Control Protocol (TCP)

## Overview
**Transmission Control Protocol (TCP)** is a **Transport Layer** protocol in both the **OSI** and **TCP/IP** models.  
It provides **reliable, ordered, and error-checked delivery of data** between applications running on different hosts.

TCP is **connection-oriented**, meaning a connection must be established before data transmission and properly terminated afterward.

---

## Key Characteristics
- Connection-oriented protocol
- Reliable data transmission
- Ordered delivery of data
- Error detection and retransmission
- Flow control and congestion control
- Data is transmitted in **segments**

---

## TCP Connection Establishment (3-Way Handshake)
Before any data is transmitted, TCP establishes a connection using a **3-way handshake**:

1. **SYN**  
   The client sends a synchronization (SYN) packet to initiate a connection.

2. **SYN-ACK**  
   The server responds with a synchronization-acknowledgment (SYN-ACK) to accept the request.

3. **ACK**  
   The client sends an acknowledgment (ACK), and the connection is established.

After this process, both sides are ready to exchange data.

---

## Data Transmission in TCP
- Application data is divided into **smaller units called segments**
- Each segment is assigned a **sequence number**
- The receiver sends an **ACK** indicating the next expected sequence number
- If a segment is lost or corrupted, TCP **retransmits** the missing data

This mechanism ensures **reliability and correct ordering** of data.

---

## Error Detection and Retransmission
- TCP uses a **checksum** to detect errors in transmitted segments
- Missing or corrupted segments are identified using **sequence numbers**
- The sender retransmits segments if acknowledgments are not received within a certain time

---

## TCP Connection Termination (4-Way Handshake)
TCP closes connections gracefully using a **4-way handshake**:

1. **FIN** – One side requests connection termination  
2. **ACK** – The other side acknowledges the request  
3. **FIN** – The second side sends its own termination request  
4. **ACK** – Final acknowledgment is sent, and the connection is closed

This ensures that all remaining data is delivered before the connection ends.

---

## Why TCP Matters in Networking & Security
- Used by critical protocols such as **HTTP, HTTPS, FTP, SMTP, and SSH**
- Essential for understanding:
  - Network troubleshooting
  - Packet analysis (Wireshark)
  - Web security
  - Exploit reliability
  - Command-and-control (C2) stability

A strong understanding of TCP is foundational for **SOC analysts, penetration testers, and Red Team professionals**.

---

## Summary
TCP ensures reliable communication by:
- Establishing connections before data transfer
- Using sequence numbers and acknowledgments
- Detecting errors and retransmitting lost data
- Closing connections gracefully

It trades speed for reliability, making it suitable for applications where accuracy matters more than latency.
