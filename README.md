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

---
## ⚙️ Key Features as of now
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
⬜ Subnetting and IP addressing  
⬜ OSPF on firewalls, routers and switches.  
⬜ and more

---
