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

---

## 🌐 IP Addressing Scheme

Each VLAN is assigned a dedicated IP subnet with a centralized default gateway on the router.  
This simplifies routing, troubleshooting, and access control enforcement.

| VLAN | Network | Default Gateway |
|----|--------|----------------|
| USERS (10) | 192.168.10.0/24 | 192.168.10.1 |
| SERVERS (20) | 192.168.20.0/24 | 192.168.20.1 |
| IT (30) | 192.168.30.0/24 | 192.168.30.1 |
| GUEST (40) | 192.168.40.0/24 | 192.168.40.1 |

---

##  Routing & DHCP

### Inter-VLAN Routing
- Implemented using **router-on-a-stick**
- A single physical router interface is divided into multiple subinterfaces
- Each subinterface acts as the default gateway for its respective VLAN
- Enables controlled communication between VLANs

### DHCP Configuration
- Centralized DHCP service hosted on the router
- Separate DHCP pools per VLAN
- Automatic IP address assignment for:
  - Users
  - IT administrators
  - Guest devices
- Reduces manual configuration errors and simplifies network management

---

## 🔐 Security Controls

### Access Control Policy
The network enforces **role-based access control** using extended ACLs to protect sensitive banking systems.

| Source VLAN | Destination | Access |
|-----------|------------|--------|
| GUEST (40) | SERVERS (20) | ❌ Denied |
| USERS (10) | SERVERS (20) | ❌ Denied |
| IT (30) | SERVERS (20) | ✅ Allowed |

### Implementation Details
- Extended ACLs applied on the router
- Traffic filtered between VLANs at Layer 3
- Least-privilege principle enforced
- Reduces lateral movement and attack surface
---

##  Validation & Testing
### Evidence

Screenshots validating the implementation are provided below:

- 📐 **Network Topology**  
  [View topology diagram](screenshots/Topology.png)

- 🌐 **DHCP Success (Users VLAN)**  
  [View DHCP assignment](screenshots/DHCP%20success.png)

- 🔐 **IT Access to Core Banking Servers**  
  [View allowed ping](screenshots/IT%20ping%20allowed.png)

- 🚫 **Blocked Access (Guest/User VLANs)**  
  [View blocked ping](screenshots/Blocked%20pings.png)

The network configuration was validated through functional and security testing to ensure correct behavior.

### Functional Tests
- DHCP successfully assigns IP addresses to all VLANs
- Inter-VLAN routing operates as expected
- Default gateways reachable from respective VLANs

### Security Tests
- Users (VLAN 10) cannot access server network (VLAN 20)
- Guests (VLAN 40) are fully isolated from internal systems
- IT administrators (VLAN 30) have authorized access to server resources

### Results
All tests behaved as expected, confirming correct network segmentation, routing, and security enforcement.
