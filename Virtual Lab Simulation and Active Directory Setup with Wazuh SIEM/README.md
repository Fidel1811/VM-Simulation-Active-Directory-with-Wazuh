# Virtual Lab Simulation and Active Directory Setup with Wazuh SIEM

This project demonstrates the setup of a virtual cybersecurity lab simulating a small enterprise network. It includes:

- **Active Directory (AD)** for centralized identity management
- **Wazuh SIEM** for host-based intrusion detection and log analysis
- Multiple virtual machines representing endpoints and infrastructure components

---

## Technologies Used

- Windows Server 2016 (Domain Controller)
- Windows 10 Pro (Client endpoint)
- Ubuntu (Wazuh Manager)
- Active Directory (AD DS)
- Wazuh SIEM
- VMware Workstation or ESXi
- AWS EC2 (optional for Wazuh cloud deployment)

---

## Lab Architecture
'''
                            +--------------------+
                            |  Ubuntu (Wazuh SIEM)|
                            |  Manager + Agents   |
                            +----------^----------+
                                       |
                                       |
+----------------+        +-----------+----------+
| Windows Server |<------>|  Windows 10 Pro      |
| (AD + DNS)     |        |  Domain-Joined Client|
+----------------+        +----------------------+
'''
         Active Directory Domain: lab.local

## Components:
- **Windows Server 2016**: Active Directory, DNS
- **Windows 10 Pro**: Joined to the domain
- **Ubuntu**: Wazuh server (manager, API, dashboard)
- All logs from endpoints are forwarded to Wazuh

---

## Project Goals

- Simulate an enterprise environment
- Deploy and configure AD on Windows Server 2016
- Join a Windows 10 client to the domain
- Set up Wazuh SIEM on Ubuntu to monitor both Windows systems
- Generate security events and analyze alerts in Wazuh

---

## System Requirements

| Machine         | vCPU | RAM  | Disk  |
|-----------------|------|------|-------|
| Domain Controller | 2    | 4GB  | 40GB  |
| Client Machine    | 2    | 2GB  | 40GB 


