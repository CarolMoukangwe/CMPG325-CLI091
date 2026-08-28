# CMPG325-CLI091
CMPG325 Network Design Project for Sebata Financial advisory (CLI-091)

1. OVERVIEW 
Sebata Financial Advisory in Kimberley will have a full network design and simulation. It provides enough networking for professional services, guarantees vital service availability, allows safe management (SSH), and comprises Guest Wi-Fi change request (CR3). Testable, functional, and documented on GitHub. 

2. TOPOLOGY - Extended Star 
Central multilayer switch 3560 as core for inter-VLAN routing. 
- 1x Multilayer Switch 3560 (Core, Inter-VLAN routing, ACL, SSH) 
- 2x 2960 Switches: LAB 2960 (VLAN 10), SERVER ROOM 2960 (VLAN 20) 
- 1x Router 1941 serves as the Internet gateway. 
- 2x Access Point0 (VLAN 30 Guest) 
- Devices: 5x wired computers (PC0-PC4), 3x servers (FILE SERVER, PRINTER SERVER, SERVER0), 1x printer (PRINTER0), 4x wireless devices (STAFF LAPTOP1, STAFF Smartphone, GUEST LAPTOP, GUEST Smartphone1). 

3. IP ADDRESSING PLAN - Only 172.30.62.0/23 

VLAN 10 - STAFF LAB: 172.30.62.0/25 
- Gateway: 172.30.62.1/25 (on Multilayer Switch) 
- Range: 172.30.62.2 - 172.30.62.126 
- Devices: PC0(10), PC1(11), PC2(12), PC3(13), PC4(14), STAFF LAPTOP1, STAFF Smartphone 
- Switch: LAB 2960 

VLAN 20 - CRITICAL SERVICES: 172.30.62.128/25 
- Gateway: 172.30.62.129/25 (on Multilayer Switch) 
- Range: 172.30.62.130–172.30.62.254 
- Devices: FILE SERVER(.130), PRINTER SERVER(.131), SERVER0, Printer0 
- Switch: SERVER ROOM 2960 
- Note: Highly available - `no shutdown` on all ports, independent VLAN. 

VLAN 30 - GUEST: 172.30.63.0/25 
Gateway: 172.30.63.1/25 (on Multilayer Switch) 
- Range: 172.30.63.2 - 172.30.63.126 
- Devices: GUEST LAPTOP, GUEST Smartphone1 
- AP: Access Point0 - SSID: `Sebata Guest` 

Router 1941 Gig1/0: 192.168.1.1/24 or DHCP to ISP (Internet access) 

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
