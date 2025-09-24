# Network-Troubleshooting-Lab
A Cisco Packet Tracer lab implementing static and dynamic (OSPF) routing protocols. This project includes network failure simulation and a step-by-step troubleshooting guide.
Network Troubleshooting Lab
Introduction
This project involved designing, configuring, and troubleshooting a multi-router network using Cisco Packet Tracer. The objective was to implement and analyze both static and dynamic routing protocols (OSPF), simulate network failures, and apply a systematic troubleshooting methodology to restore connectivity. This project demonstrates a foundational understanding of network operations, routing logic, and fault analysis.



Network Topology
The network was built using three routers, two switches, and two PCs to simulate two distinct local area networks (LANs) connected via a wide area network (WAN).

IP Addressing and Configuration
Each device was configured with a static IP address to enable communication. Routers were configured via the Command Line Interface (CLI) to assign IP addresses to their interfaces. The detailed IP addressing scheme is outlined in the tables on pages 1 and 2 of the project report.



Routing Protocol Configuration
Static Routing
Initially, static routes were configured to establish a baseline for connectivity. This involved manually defining the path on each router to reach non-directly connected networks. A successful 


ping confirmed that the static routes were working correctly.


Dynamic Routing (OSPF)
To enable the network to adapt to changes automatically, the static routes were removed and the OSPF dynamic routing protocol was configured. All routers were placed in 

area 0. The 

show ip route command on router R1 confirmed that it learned routes to the other LANs via OSPF.

Network Troubleshooting
A network failure was simulated by shutting down the 

GigabitEthernet0/0 interface on router R1. This led to a failed 

ping between the two PCs.


Investigation: The troubleshooting process involved using traceroute to identify the point of failure, show ip route to confirm the missing route, and show ip ospf neighbor to check for lost neighbor relationships.


Root Cause: The show ip interface brief command on R1 revealed that the GigE0/0 interface was administratively down.


Resolution: The issue was resolved by re-enabling the interface with the no shutdown command, which restored connectivity.

Automation for Error Detection
To proactively monitor the network, an automation script using Python could be developed. The script could be scheduled to run every 15 minutes, connect to all routers via SSH, and execute the 

show ip ospf neighbor command. If the script detects fewer neighbors than expected, it could send an email alert to the network administrator, allowing for much faster detection of link failures.


Conclusion
This project successfully demonstrated the entire process of network configuration, from design to troubleshooting. The key takeaways are the efficiency of dynamic routing protocols like OSPF over static routing and the importance of a logical, layer-by-layer troubleshooting methodology.
