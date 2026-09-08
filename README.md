# Enterprise-Network
A Cisco Packet Tracer enterprise networking lab designed to apply CCNA-level routing, switching, network services, and security concepts in a multi-site environment.

The network uses a redundant three-tier architecture with an edge router, dual core switches, redundant distribution switches, multiple access switches, dual ISP connections, segmented user networks, VoIP, wireless infrastructure, and centralized services.

The project includes VLAN segmentation, inter-VLAN routing, dynamic routing, spanning tree, EtherChannel, DHCP, NAT, ACLs, IPv4/IPv6 addressing, and network redundancy.

This lab was completed as part of my CCNA preparation using Jeremy's IT Lab's Mega Lab and expanded/documented as a portfolio project.

## <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/tree/main/Topology">Network Topology</a>
<img width="1112" height="708" alt="Screenshot 2026-09-08 095334" src="https://github.com/user-attachments/assets/9e7723a0-7194-464c-a8b4-5000f9c0cb8f" />

## Technologies / Concepts
- Cisco IOS
- Cisco Packet Tracer
- IPv4 and IPv6
- Subnetting
- VLANs and trunking
- Inter-VLAN routing
- Spanning Tree Protocol (STP)
- EtherChannel
- OSPF
- Static and default routing
- DHCP
- DNS
- NAT/PAT
- Access Control Lists (ACLs)
- First-Hop Redundancy
- Network device hardening
- Layer 2 and Layer 3 troubleshooting
## <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/blob/main/Documentation/architecture.md">Architecture</a>
The network follows a hierarchical enterprise design consisting of an edge, core, distribution, and access layer.

R1 provides connectivity between the internal network and two simulated ISPs. CSW1 and CSW2 form the redundant Layer 3 core and connect to both distribution switch pairs. Each office uses two distribution switches to provide redundant routing and first-hop gateway services through HSRP.

Access switches provide connectivity for user workstations, IP phones, wireless infrastructure, and servers. VLAN segmentation separates user, voice, server, wireless, and network-management traffic.
## <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/blob/main/Documentation/addressing-plan.md">Network Segmentation</a>
| Network         | VLAN | Subnet         | Virtual Gateway |
| --------------- | ---: | -------------- | --------------- |
| Office A PCs    |   10 | `10.1.0.0/24`  | `10.1.0.1`      |
| Office A Phones |   20 | `10.2.0.0/24`  | `10.2.0.1`      |
| Office B PCs    |   10 | `10.3.0.0/24`  | `10.3.0.1`      |
| Office B Phones |   20 | `10.4.0.0/24`  | `10.4.0.1`      |
| Servers         |   30 | `10.5.0.0/24`  | `10.5.0.1`      |
| Wi-Fi           |   40 | `10.6.0.0/24`  | `10.6.0.1`      |
| Management A    |   99 | `10.0.0.0/28`  | `10.0.0.1`      |
| Management B    |   99 | `10.0.0.16/28` | `10.0.0.17`     |

## <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/tree/main/Verification">Verification</a>
The completed network was validated using Cisco IOS verification commands and end-to-end connectivity testing.

Key checks included:
<ul>
  <li>Verified OSPF neighbor adjacencies and dynamically learned routes</li>
  <li>Confirmed HSRP active/standby gateway redundancy</li>
  <li>Validated EtherChannel formation between redundant switches</li>
  <li>Verified VLAN, trunking, and spanning-tree operation</li>
  <li>Confirmed NAT/PAT translations at the Internet edge</li>
  <li>Tested end-to-end connectivity between internal networks and external destinations</li>
</ul>

Supporting command output and connectivity tests are available in the <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/tree/main/Verification">verification/ directory</a>.

## <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/blob/main/Documentation/troubleshooting.md">Troubleshooting</a>
During this lab 2 major configuration and connectivity issues were diagnosed and resolved during implementation of the lab.

Troubleshooting involved validating Layer 1–3 connectivity, reviewing interface and VLAN configurations, checking routing and redundancy protocols, and using Cisco IOS diagnostic commands to isolate configuration errors.

Detailed troubleshooting examples, including symptoms, root causes, resolutions, and verification steps, are documented in <a href="https://github.com/Daniel-Carbajal/Enterprise-Network/blob/main/Documentation/troubleshooting.md">documentation/troubleshooting.md</a>.

## What I Learned
- Configured and troubleshot Cisco routers and switches through IOS CLI
- Designed and implemented VLAN segmentation and 802.1Q trunking
- Configured Layer 3 routing between multiple network segments
- Implemented dynamic routing using OSPF
- Configured redundant Layer 2 paths using STP
- Built aggregated switch links using EtherChannel
- Implemented DHCP, NAT/PAT, and access control policies
- Verified network operation using Cisco IOS diagnostic commands
- Diagnosed Layer 2 and Layer 3 connectivity issues
- Documented network topology, addressing, configurations, and validation

## Credits
The original Mega Lab topology and lab requirements were created by
Jeremy's IT Lab as part of his free CCNA course.

This repository documents my implementation, configurations,
verification, troubleshooting, and analysis of the lab.
