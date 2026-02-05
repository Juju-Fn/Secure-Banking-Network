#  Secure Banking Network Design (Cisco Packet Tracer)

## 📌 Overview
This project simulates a **secure enterprise banking network** designed and implemented using **Cisco Packet Tracer**.  
The focus is on **network segmentation, controlled access, and least-privilege security**, mirroring how real banking branch networks are built and protected.

The network enforces **role-based access control** between users, IT administrators, guests, and core banking systems.

---

## Project Objectives
- Design a realistic banking network topology
- Segment the network using VLANs
- Enable inter-VLAN routing using router-on-a-stick
- Implement centralized DHCP
- Enforce bank-grade access control policies
- Prevent unauthorized access to sensitive systems

---

## 🧱 Network Architecture

### Core Design
- **Router:** Cisco ISR4331
- **Core Switch:** SW_USERS (Cisco 2960)
- **Access Switches:**
  - SW_SERVERS (Server network)
  - SW_GUEST (Guest network)

### Design Approach
- Core / access switch architecture
- Centralized routing using router-on-a-stick
- Logical segmentation enforced at Layer 2 and Layer 3
- Architecture mirrors small-to-medium banking branch deployments

---

##  VLAN Design

The network is segmented using VLANs to isolate users, servers, IT administration, and guest devices.  
This limits lateral movement and enforces least-privilege access.

| VLAN ID | Name    | Purpose |
|-------|--------|--------|
| 10 | USERS | Teller and employee workstations |
| 20 | SERVERS | Core banking systems |
| 30 | IT | IT administration and management |
| 40 | GUEST | Guest and visitor devices |

