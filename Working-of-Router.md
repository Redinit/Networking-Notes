# Working of Routers

![Router](./Images/wifi-router.png)

## 🌐 Purpose of a Router
- Connects **different networks** (LANs, WANs, Internet).
- Forwards **packets** based on **IP addresses**.
- Works at **Layer 3 (Network Layer)** of OSI.

## 🔹 Why IP is Used
- **MAC addresses**: Physical, used in LANs, identify devices locally.
- **IP addresses**: Logical, used across networks, identify devices globally.
- IP allows packets to travel **between networks**, not just within one LAN.

## 🔹 Packet Forwarding (Hop by Hop)
1. Packet arrives at router → router examines **destination IP**.
2. **Routing table check**:
   - If **directly connected network** → deliver directly.
   - If **route exists** → forward to **next hop**.
   - If **no route** → forward to **default gateway** (if configured) or **drop packet**.
3. Each intermediate router repeats this **hop-by-hop** forwarding until the packet reaches the destination network.
4. When the packet reaches the **destination network**, the local **switch delivers it using MAC addresses**.

## 🔹 Routing Table
- Stores **routes to different networks**.
- Each entry contains:
  - **Destination network**
  - **Next hop or outgoing interface**
  - **Metric** (used to choose best path)
- Routes can be:
  - **Static**: manually configured
  - **Dynamic**: learned via routing protocols like RIP, OSPF, BGP

## 🔹 How Best Path is Chosen
- Routers use **metrics** (hop count, bandwidth, delay) to select paths.
- **Lower metric** = preferred route.
- Dynamic routing allows routers to **learn new paths** automatically.

## 🔹 Example Scenarios
- **Same LAN**: PC1 → PC2
  - Router not needed.
  - Switch uses **MAC addresses** to forward frames.
- **Different Network**: PC1 → PC3
  - PC1 sends packet to **default gateway (router)**.
  - Router forwards packet **hop-by-hop** based on routing tables.
  - Final router delivers packet to **destination switch**, then **MAC forwards to PC3**.

## 🔹 Key Concepts
- **Hop-by-hop forwarding**: Each router checks routing table and forwards packet toward destination.
- **TTL (Time to Live)**: Ensures packets don’t loop forever; discarded when TTL = 0.
- **Post office analogy**: Router = internet’s post office → receives packets, checks addresses, forwards along the correct path.

---

**Summary**: Routers enable communication across networks by using IP addresses, forwarding packets hop-by-hop, and choosing the best path using routing tables and protocols. MAC addresses are used only inside local networks for delivery once the packet reaches its destination LAN.
