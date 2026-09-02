# Secure Business Network System (in progress)

## 📌 Overview
This project focuses on designing a **secure and scalable enterprise network** for a multi-floor business building. The design ensures **high availability, redundancy, and robust security** against both internal and external threats.

---
## 🏢 Building Structure
The business infrastructure spans **three floors**, hosting the following departments:
- Marketing & Sales  
- Human Resources (HR) & Logistics  
- Finance & Accounting  
- Administration & Public Relations  
- ICT Department  
- Server Room  

---
## 🔐 Security Architecture
To safeguard the network, multiple layers of security are implemented:
- Dual firewall setup for perimeter protection  
- DMZ (Demilitarized Zone) for public-facing services  
- Active Directory-based centralized authentication  
- Network segmentation using VLANs  
- Protection against both internal and external threats  

---
## 🌐 Network Infrastructure
### Internet Connectivity
- Dual ISP setup for redundancy:
  - Airtel Business  
  - Jio Business
### Security Devices
- 2 × Cisco ASA 5506-X Firewalls  
### Switching Infrastructure
- 2 × Cisco Catalyst 3650 (48-port) switches  
- Cisco Catalyst 2960 (48-port) switches  
### Wireless Infrastructure
- Cisco Wireless LAN Controller (WLC)  
- Lightweight Access Points (LAPs)
### Communication
- Cisco Voice Gateway for IP Telephony
### Servers
- Physical servers used for virtualization  
- Hosting services such as:
  - Active Directory  
  - DNS, DHCP  
  - File services  
  - Other enterprise applications  
---

## 🧩 Network Segmentation (VLANs)
| VLAN Name  | VLAN ID| Purpose                          |
|------------|--------|----------------------------------|
| Management | 10     | Network device management        |
| LAN        | 20     | Wired user network               |
| WLAN       | 50     | Wireless user network            |
| VoIP       | 70     | IP Telephony                     |
| Inside Svr | 90     | Internal Server Infra            |
| Blackhole  | 199    | Unused ports (security isolation)|

---
<img width="2668" height="1934" alt="Network Topology Design" src="https://github.com/user-attachments/assets/45f9256e-a482-4bd0-a001-f2134fba9680" />

---

## ⚙️ Fundamental Device Configuration
Configured baseline administrative and security settings across all network devices, including:
- Unique hostnames to switches and networking devices
- Console access passwords
- MOTD (Message of the Day) banner warnings
- Executive session timeout for inactive management sessions
- Enabled logging synchronous for improved CLI usability
- Disabled automatic DNS resolution on switches to improve CLI response time and prevent unnecessary DNS lookups
---
## 🔐 Secure Remote Management
Implemented secure remote administration features by configuring SSH-based access for secure device management. Additionally, a standard Access Control List (ACL) was implemented to restrict administrative access, ensuring that only devices within the dedicated management VLAN/network are authorized to perform remote management operations.

---
## 🌐 VLAN & Switching Configuration
Configured Layer 2 and Layer 3 switching infrastructure. Established trunk links between switches, configured VLAN assignments and assigned access ports to appropriate VLANs based on connected devices and departments.

<img width="964" height="646" alt="Screenshot 2026-05-13 201239" src="https://github.com/user-attachments/assets/f567381c-2039-40ba-9ce1-7be84cd57c43" />
<img width="964" height="648" alt="image" src="https://github.com/user-attachments/assets/62fd0126-ef02-42e1-9a15-4760e15705b0" />
<img width="452" height="598" alt="Screenshot 2026-05-13 195434" src="https://github.com/user-attachments/assets/00f8c1ca-afe3-47df-a80a-a3d3b8115021" />

## EtherChannel & Link Aggregation

* **Link Bundling (LACP)**: Configured LACP (IEEE 802.3ad) across interfaces `Gig1/0/9 - 11` on both Multi-Layer Switches (`MLSW1` & `MLSW2`) to aggregate bandwidth, establish redundancy and create logical link `Port-Channel 1` (`Po1`).
* **Load-Balancing Algorithm**: Set frame distribution to `src-mac` (Source MAC address hashing) to balance outbound traffic streams across the physical member links based on the originating device's hardware address.
* **Spanning Tree Protocol (STP) Behavior**: STP treats the bundled ports as a single logical link (`Po1`), preventing Layer 2 loops while allowing standard blocking (`Altn BLK`) and forwarding (`Desg FWD`) roles on the aggregate interface.
* **Verification Commands**:
  ```cisconetwork
  Switch# show etherchannel summary
  Switch# show etherchannel load-balance
  ```

## Network Addressing & Subnet Architecture

### Enterprise Subnet Allocation
| Category | Network & Subnet Mask | Valid Host Addresses | Default Gateway | Broadcast Address |
| :--- | :--- | :--- | :--- | :--- |
| **Management** | `192.168.10.0/24` | `192.168.10.1` to `192.168.10.254` | `192.168.10.1` | `192.168.10.255` |
| **WLAN** | `10.20.0.0/16` | `10.20.0.1` to `10.20.255.254` | `10.20.0.1` | `10.20.255.255` |
| **LAN** | `172.16.0.0/16` | `172.16.0.1` to `172.16.255.254` | `172.16.0.1` | `172.16.255.255` |
| **VOIP** | `172.30.0.0/16` | `172.30.0.1` to `172.30.255.254` | `172.30.0.1` | `172.30.255.255` |
| **DMZ** | `10.11.11.0/27` | `10.11.11.1` to `10.11.11.30` | `10.11.11.1` | `10.11.11.31` |
| **INSIDE SERVERS** | `10.11.11.32/27` | `10.11.11.33` to `10.11.11.62` | `10.11.11.33` | `10.11.11.63` |

---

### Point-to-Point Interconnects (Edge & Core)

> **Implementation Note:** Firewall segments listed below reflect planned network boundaries and reserved `/30` subnets. Active routing is currently configured across MLSWs, Edge Routers, and Internet Clients.

| Segment | Subnet | Status / Assignment |
| :--- | :--- | :--- |
| **CLOUD Area** | `8.0.0.0/8` | Active |
| **ISP1 - Internet** | `20.20.20.0/30` | Active |
| **ISP2 - Internet** | `30.30.30.0/30` | Active |
| **ISP1 to FWL1** | `105.100.50.0/30` | Reserved (Firewall Phase) |
| **ISP1 to FWL2** | `105.100.50.4/30` | Reserved (Firewall Phase) |
| **ISP2 to FWL1** | `205.200.100.0/30` | Reserved (Firewall Phase) |
| **ISP2 to FWL2** | `205.200.100.4/30` | Reserved (Firewall Phase) |
| **FWL1 to MLSW1** | `10.2.2.0/30` | Reserved / Direct Router transit |
| **FWL1 to MLSW2** | `10.2.2.4/30` | Reserved / Direct Router transit |
| **FWL2 to MLSW1** | `10.2.2.8/30` | Reserved / Direct Router transit |
| **FWL2 to MLSW2** | `10.2.2.12/30` | Reserved / Direct Router transit |

* **Verification of Subnetting :** 
```cisconetwork 
Switch# show ip interface brief 
``` 

> ### 💡 What i learned about subnetting for point-to-point Links
> 
> * **Standard Approach (`/30`)**: Point-to-point connections only require 2 usable host IP addresses. Traditionally, a `/30` subnet is assigned (4 total IP addresses: 1 network ID, 2 usable host IPs, and 1 broadcast address).
> * **Optimized Approach (`/31`)**: Defined by **RFC 3021**, `/31` subnets drop the requirement for separate network and broadcast addresses on point-to-point links. Both available IP addresses are used as valid host addresses, cutting IP waste by 50%.
> * **Note**: Cisco packet tracer do not support RFC 3021 so i stick with /30 for point-to-point links.

---

## First Hop Redundancy Protocol (HSRP) & Gateway Load Sharing
![alt text](/img/image.png)
To eliminate single points of failure at the default gateway level, Hot Standby Router Protocol (HSRP) is configured across `CORE-SW1` and `CORE-SW2`. An **Active/Active gateway load-sharing** strategy is implemented to distribute traffic processing across both distribution switches rather than leaving hardware idle.

* **Deterministic Failover**: Gateways role are explicitly assigned using HSRP priorities so that it can be configured easily without having to rely on the default IP address for failover. 
Primary switches automatically reclaim the Active gateway role upon recovering from a failure.
* **Gateway Distribution Matrix**:
  * **CORE-SW1 (Primary Gateway)**: Active for **VLAN 10** (Management) and **VLAN 20** (LAN). Standby for VLANs 50 and 90.
  * **CORE-SW2 (Primary Gateway)**: Active for **VLAN 50** (WLAN) and **VLAN 90** (VOIP). Standby for VLANs 10 and 20.

* **Verification of Hop Redundancy**
```cisconetwork 
show standby brief
```
---

## ⚙️ Key Features
- Redundant internet connectivity using dual ISP architecture
- Secure network segmentation through VLAN implementation 
- Centralized authentication via Active Directory
- SSH-enabled secure remote device administration
- ACL-based restriction for administrative access    
- Integrated wired, wireless, and VoIP infrastructure  

---
## 🚧 Project Status
✅ Network topology design and VLAN segmentation.  
✅ Trunking configuration and baseline switch configuration.  
✅ SSH remote access and administrative ACLs.  
✅ Subnetting and IP addressing  
✅ First Hop Redundancy Protocol (HSRP) & Gateway Load Sharing  
⬜ OSPF on firewalls, routers and switches.  
⬜ and more

---
