# CMPG325-CLI091
CMPG325 Network Design Project for Sebata Financial advisory (CLI-091)

1. OVERVIEW 
Sebata Financial Advisory is a professional financial services firm opening a new branch in 
Kimberley. They handle sensitive client financial data, which requires a secure, highly 
available, and segregated network. The firm has requested a full network design and 
simulation in Cisco Packet Tracer.
 
BUSSNESS REQUIREMENTS 
Staff operations : 
The firm needs wired lab for 5 staff pcs, 1 staff laptop and 1 smartphone for daily financial 
operations. 
Critical services : 
Files, print and application servers must be available throughout business hours ( 08:00
17:00) without downtime. 
Guest Access : 
Following client change request CR3, guests in reception require isolated Wi-Fi that cannot 
access internal financial systems. 
Secure management: 
All network devices must be managed securely due to POPIA compliance.

NETWORK DESIGN -EXTENDED STAR TOPOLOGY 
A central multilayer switch 3560 is deployed as the core layer to provide inter-VLAN routing 
(sebatacore). -core 1x multilayer switch 3560 -Distribution 2x 2960 switches (lab switch and server room switch) -Edge 1x router 1941 internet edge ,2x Access points 9 staff and guest) -End devices 5x wired PCs, 1x staff laptop, 1x staff smartphone, 1x guest laptop,1x guest 
smartphone ,3x servers, 1x printer. 
All  edge devices connect back to the core switch forming an extended star , ensuring 
single point of management and easy troubleshooting.
