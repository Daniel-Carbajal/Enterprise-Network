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
## Architecture
The network follows a hierarchical enterprise design consisting of an edge, core, distribution, and access layer.

R1 provides connectivity between the internal network and two simulated ISPs. CSW1 and CSW2 form the redundant Layer 3 core and connect to both distribution switch pairs. Each office uses two distribution switches to provide redundant routing and first-hop gateway services through HSRP.

Access switches provide connectivity for user workstations, IP phones, wireless infrastructure, and servers. VLAN segmentation separates user, voice, server, wireless, and network-management traffic.
## Configuration Highlights

## Verification

## Troubleshooting

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
