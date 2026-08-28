# CMPG325-CLI091
CMPG325 Network Design Project for Sebata Financial advisory (CLI-091)

1. OVERVIEW 
Sebata Financial Advisory in Kimberley will have a full network design and simulation. It provides enough networking for professional services, guarantees vital service availability, allows safe management (SSH), and comprises Guest Wi-Fi change request (CR3). Testable, functional, and documented on GitHub. 

2. TOPOLOGY - Extended Star 
Central multilayer switch 3560 as core for inter-VLAN routing. 
- 1x Multilayer Switch 3560 (Core, Inter-VLAN routing, ACL, SSH) 
- 2x 2960 Switches: LAB 2960 , SERVER ROOM 2960 (VLAN 20) 
- 1x Router 1941 serves as the Internet gateway. 
- 2x Access Point0 
- Devices: 5x wired computers (PC0-PC4), 3x servers (FILE SERVER, PRINTER SERVER, SERVER0), 1x printer (PRINTER0), 4x wireless devices (STAFF LAPTOP1, STAFF Smartphone, GUEST LAPTOP, GUEST Smartphone1). 

3. IP ADDRESSING PLAN - Only 172.30.62.0/23 

Topology 1: VLAN 30 (GUEST / Wireless - Extended Star) 
- Network: 172.30.62.0/25 
- Subnet Mask: 255.255.255.128 
- Gateway: 172.30.62.1 
- Usable Range: 172.30.62.2 - 172.30.62.126 
- Devices: 
- PC0: 172.30.62.10 / 255.255.255.128 / GW 172.30.62.1 
- STAFF LAPTOP1: 172.30.62.20 / 255.255.255.128 / GW 172.30.62.1 

Topology 2 - VLAN 99 (MANAGEMENT / Native) 
- Network: 172.30.62.64/26 (Reserved within /25) 
- Subnet Mask: 255.255.255.192 
- Gateway: 172.30.62.65 
- Devices: Management IPs of Switches (3560, 2960) 
- Objective: AdminCM SSH management 

Topology 3 - VLAN 20 (CRITICAL SERVICES - Shared) 
- Network: 172.30.62.128/25 
- Subnet Mask: 255.255.255.128 
Gateway: 172.30.62.129 
- Usable Range: 172.30.62.130 - 172.30.62.254 

Topology 4 - VLAN 30 (FILE SERVICES / SERVER FARM) 
- Network: 172.30.63.0/25 
- Subnet Mask: 255.255.255.128 
Gateway: 172.30.63.1 
- Usable Range: 172.30.63.2 - 172.30.63.126 
- Devices: 
- FILE SERVER: 172.30.63.10 / 255.255.255.128 / GW 172.30.63.1 
- GUEST LAPTOP: Proposed IP 172.30.63.11; this device will be on the same VLAN to test internet access. 
- Justification: To keep File server separate from personnel 62.0/25, it is put in the 63.0/25 subnet. It is still inside the assigned 62.0/23 super-block. ACL GUEST-ISOLATION regulates privileges.

4. DESIGN RESTRICTION - Critical Service Availability 
File, print, and application services should be available during business hours. 

Realization: 
- Dedicated SERVER ROOM 2960 Switch solely for VLAN 20 
- All server ports configured to `no shutdown` are not impacted by modifications to LAB or GUEST settings. 
- Core Multilayer Switch changes for SSH and Guest ACL performed without SERVER ROOM switch reboots. 
- The gateways for VLAN 20 are always available. 

5. SSH: NETWORKING CHALLENGE (Intermediate) 

Requirement: Lock device management, turn off Telnet. 

Multilayer Switch 3560 (and Router) configuration
