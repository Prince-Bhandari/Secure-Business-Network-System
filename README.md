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
  - DNS / DHCP  
  - File services  
  - Other enterprise applications  

---

## 🧩 Network Segmentation (VLANs)

| VLAN Name   | VLAN ID | Purpose                          |
|------------|--------|----------------------------------|
| Management | 10     | Network device management        |
| LAN        | 20     | Wired user network               |
| WLAN       | 50     | Wireless user network            |
| VoIP       | 70     | IP Telephony                     |
| Blackhole  | 199    | Unused ports (security isolation)|

---

## ⚙️ Key Features as of now
- High availability using dual ISPs  
- Secure network segmentation with VLANs  
- Centralized authentication via Active Directory  
- Scalable design for enterprise environments  
- Integrated wired, wireless, and VoIP infrastructure  

---

## 🚧 Project Status
✅ Network design and component arrangement completed  
⬜ Implementation and configuration in progress  

---

<img width="2669" height="1931" alt="Network-Design-and-Arrangement-of-Components" src="https://github.com/user-attachments/assets/35dc725d-8fc0-4261-ab39-5960c501005a" />

---
