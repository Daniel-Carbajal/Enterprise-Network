# Network Architecture

The Enterprise Network Mega Lab uses a hierarchical network design consisting of edge, core, distribution, and access layers.

## Edge Layer

R1 acts as the enterprise edge router and connects the internal network to two simulated Internet service providers. It also provides connectivity to both core switches and performs functions such as external routing and NAT/PAT.

## Core Layer

CSW1 and CSW2 form the redundant Layer 3 core.

Both core switches connect to R1 and all four distribution switches. A Layer 3 EtherChannel between CSW1 and CSW2 provides additional connectivity and redundancy within the core.

OSPF is used to exchange routes throughout the Layer 3 infrastructure.

## Distribution Layer

Each office contains two distribution switches:

* Office A: DSW-A1 and DSW-A2
* Office B: DSW-B1 and DSW-B2

The distribution switches provide inter-VLAN routing and redundant default gateways using HSRP.

Each distribution switch also maintains routed connectivity to both core switches, preventing a single uplink failure from isolating an office.

## Access Layer

Each office contains three access switches.

Access switches are dual-homed to both distribution switches and provide connectivity for:

* User workstations
* IP phones
* Wireless infrastructure
* Servers
* Network management devices

VLANs and 802.1Q trunking are used to separate traffic between different network functions.

## Redundancy

The topology implements redundancy at multiple layers through:

* Dual ISP connectivity
* Dual core switches
* Dual distribution switches per office
* Dual-homed access switches
* EtherChannel
* HSRP
* Rapid PVST+
* Dynamic routing with OSPF

Together, these technologies provide alternate paths and reduce dependence on individual links or network devices.

