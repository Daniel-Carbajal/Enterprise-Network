# Physical Connections

This document provides a reference for the physical interface connections used throughout the Enterprise Network Mega Lab.

The network follows a hierarchical design consisting of an edge router, redundant core switches, redundant distribution switches for Offices A and B, and dual-homed access switches. EtherChannel links provide additional redundancy between the core switches and between each pair of distribution switches.

---

## Edge and ISP Connections

| Device | Interface | Connected Device | Remote Interface |
| ------ | --------- | ---------------- | ---------------- |
| R1     | G0/0/0    | ISPA             | —                |
| R1     | G0/1/0    | ISPB             | —                |
| R1     | G0/0      | CSW1             | G1/0/1           |
| R1     | G0/1      | CSW2             | G1/0/1           |

R1 provides redundant upstream connectivity through two simulated Internet service providers while maintaining separate routed links to both core switches.

---

## Core Layer

### CSW1 Connections

| Local Interface | Connected Device | Remote Interface | Purpose                      |
| --------------- | ---------------- | ---------------- | ---------------------------- |
| G1/0/1          | R1               | G0/0             | Routed uplink to edge router |
| G1/0/2          | CSW2             | G1/0/2           | PortChannel1 member          |
| G1/0/3          | CSW2             | G1/0/3           | PortChannel1 member          |
| G1/1/1          | DSW-A1           | G1/1/1           | Routed distribution uplink   |
| G1/1/2          | DSW-A2           | G1/1/1           | Routed distribution uplink   |
| G1/1/3          | DSW-B1           | G1/1/1           | Routed distribution uplink   |
| G1/1/4          | DSW-B2           | G1/1/1           | Routed distribution uplink   |

### CSW2 Connections

| Local Interface | Connected Device | Remote Interface | Purpose                      |
| --------------- | ---------------- | ---------------- | ---------------------------- |
| G1/0/1          | R1               | G0/1             | Routed uplink to edge router |
| G1/0/2          | CSW1             | G1/0/2           | PortChannel1 member          |
| G1/0/3          | CSW1             | G1/0/3           | PortChannel1 member          |
| G1/1/1          | DSW-A1           | G1/1/2           | Routed distribution uplink   |
| G1/1/2          | DSW-A2           | G1/1/2           | Routed distribution uplink   |
| G1/1/3          | DSW-B1           | G1/1/2           | Routed distribution uplink   |
| G1/1/4          | DSW-B2           | G1/1/2           | Routed distribution uplink   |

---

## Core EtherChannel

CSW1 and CSW2 are connected using a two-link EtherChannel.

| Port Channel | CSW1 Interfaces | CSW2 Interfaces |
| ------------ | --------------- | --------------- |
| PortChannel1 | G1/0/2, G1/0/3  | G1/0/2, G1/0/3  |

The logical PortChannel provides a redundant connection between the two core switches while allowing the physical links to operate as a single logical interface.

---

# Office A

Office A contains two redundant distribution switches and three access switches.

Each access switch is dual-homed to both distribution switches, providing redundant Layer 2 paths toward the distribution layer.

## DSW-A1 Connections

| Local Interface | Connected Device | Remote Interface | Purpose              |
| --------------- | ---------------- | ---------------- | -------------------- |
| G1/0/1          | ASW-A1           | G0/1             | Access switch uplink |
| G1/0/2          | ASW-A2           | G0/1             | Access switch uplink |
| G1/0/3          | ASW-A3           | G0/1             | Access switch uplink |
| G1/0/4          | DSW-A2           | G1/0/4           | PortChannel1 member  |
| G1/0/5          | DSW-A2           | G1/0/5           | PortChannel1 member  |
| G1/1/1          | CSW1             | G1/1/1           | Routed core uplink   |
| G1/1/2          | CSW2             | G1/1/1           | Routed core uplink   |

## DSW-A2 Connections

| Local Interface | Connected Device | Remote Interface | Purpose              |
| --------------- | ---------------- | ---------------- | -------------------- |
| G1/0/1          | ASW-A1           | G0/2             | Access switch uplink |
| G1/0/2          | ASW-A2           | G0/2             | Access switch uplink |
| G1/0/3          | ASW-A3           | G0/2             | Access switch uplink |
| G1/0/4          | DSW-A1           | G1/0/4           | PortChannel1 member  |
| G1/0/5          | DSW-A1           | G1/0/5           | PortChannel1 member  |
| G1/1/1          | CSW1             | G1/1/2           | Routed core uplink   |
| G1/1/2          | CSW2             | G1/1/2           | Routed core uplink   |

---

## Office A Distribution EtherChannel

DSW-A1 and DSW-A2 are connected using a two-link EtherChannel.

| Port Channel | DSW-A1 Interfaces | DSW-A2 Interfaces |
| ------------ | ----------------- | ----------------- |
| PortChannel1 | G1/0/4, G1/0/5    | G1/0/4, G1/0/5    |

---

## ASW-A1 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-A1           | G1/0/1           |
| G0/2            | DSW-A2           | G1/0/1           |
| F0/1            | LWAP1            | —                |
| F0/2            | WLC1             | —                |

ASW-A1 is dual-homed to both Office A distribution switches and provides access-layer connectivity for wireless infrastructure.

---

## ASW-A2 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-A1           | G1/0/2           |
| G0/2            | DSW-A2           | G1/0/2           |
| F0/1            | Phone1           | —                |

ASW-A2 is dual-homed to both Office A distribution switches and provides connectivity for an IP phone and its associated user network.

---

## ASW-A3 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-A1           | G1/0/3           |
| G0/2            | DSW-A2           | G1/0/3           |
| F0/1            | Phone2           | —                |

ASW-A3 is dual-homed to both Office A distribution switches and provides connectivity for an additional IP phone and user segment.

---

# Office B

Office B uses the same redundant distribution/access design as Office A.

Three access switches are dual-homed to DSW-B1 and DSW-B2, while both distribution switches maintain independent routed connections to both core switches.

## DSW-B1 Connections

| Local Interface | Connected Device | Remote Interface | Purpose              |
| --------------- | ---------------- | ---------------- | -------------------- |
| G1/0/1          | ASW-B1           | G0/1             | Access switch uplink |
| G1/0/2          | ASW-B2           | G0/1             | Access switch uplink |
| G1/0/3          | ASW-B3           | G0/1             | Access switch uplink |
| G1/0/4          | DSW-B2           | G1/0/4           | PortChannel1 member  |
| G1/0/5          | DSW-B2           | G1/0/5           | PortChannel1 member  |
| G1/1/1          | CSW1             | G1/1/3           | Routed core uplink   |
| G1/1/2          | CSW2             | G1/1/3           | Routed core uplink   |

## DSW-B2 Connections

| Local Interface | Connected Device | Remote Interface | Purpose              |
| --------------- | ---------------- | ---------------- | -------------------- |
| G1/0/1          | ASW-B1           | G0/2             | Access switch uplink |
| G1/0/2          | ASW-B2           | G0/2             | Access switch uplink |
| G1/0/3          | ASW-B3           | G0/2             | Access switch uplink |
| G1/0/4          | DSW-B1           | G1/0/4           | PortChannel1 member  |
| G1/0/5          | DSW-B1           | G1/0/5           | PortChannel1 member  |
| G1/1/1          | CSW1             | G1/1/4           | Routed core uplink   |
| G1/1/2          | CSW2             | G1/1/4           | Routed core uplink   |

---

## Office B Distribution EtherChannel

DSW-B1 and DSW-B2 are connected using a two-link EtherChannel.

| Port Channel | DSW-B1 Interfaces | DSW-B2 Interfaces |
| ------------ | ----------------- | ----------------- |
| PortChannel1 | G1/0/4, G1/0/5    | G1/0/4, G1/0/5    |

---

## ASW-B1 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-B1           | G1/0/1           |
| G0/2            | DSW-B2           | G1/0/1           |
| F0/1            | LWAP2            | —                |

ASW-B1 is dual-homed to both Office B distribution switches and provides connectivity for a lightweight wireless access point.

---

## ASW-B2 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-B1           | G1/0/2           |
| G0/2            | DSW-B2           | G1/0/2           |
| F0/1            | Phone3           | —                |

ASW-B2 is dual-homed to both Office B distribution switches and provides connectivity for an IP phone and its associated user network.

---

## ASW-B3 Connections

| Local Interface | Connected Device | Remote Interface |
| --------------- | ---------------- | ---------------- |
| G0/1            | DSW-B1           | G1/0/3           |
| G0/2            | DSW-B2           | G1/0/3           |
| F0/1            | SRV1             | —                |

ASW-B3 is dual-homed to both Office B distribution switches and provides access-layer connectivity for the server network.

---

# Connection Summary

The primary physical topology can be summarized as:

```text
                           +------ ISPA
                           |
                           | G0/0/0
                          R1
                           | G0/1/0
                           |
                           +------ ISPB
                          / \
                         /   \
                     CSW1=====CSW2
                      /|\       /|\
                     / | \     / | \
                    /  |  \   /  |  \
                   /   |   \ /   |   \
              DSW-A1===DSW-A2   DSW-B1===DSW-B2
                |\ |\   /| /|     |\ |\   /| /|
                | \| \ / |/ |     | \| \ / |/ |
                |  |  X  |  |     |  |  X  |  |
                | /| / \ |\ |     | /| / \ |\ |
                |/ |/   \| \|     |/ |/   \| \|
             ASW-A1    ASW-A2    ASW-B1    ASW-B2
                \        /          \          /
                 \      /            \        /
                  ASW-A3              ASW-B3
```

> The diagram above is a simplified logical representation. Refer to the main Packet Tracer topology image for the complete physical layout and endpoint placement.

---

# Redundancy Design

The physical topology contains redundancy at several layers:

* **Internet edge:** R1 connects to two simulated ISPs.
* **Core:** R1 maintains separate connections to CSW1 and CSW2.
* **Core interconnection:** CSW1 and CSW2 use a two-link EtherChannel.
* **Core-to-distribution:** Every distribution switch maintains an independent routed connection to both core switches.
* **Distribution:** Each office's distribution switches are connected with a two-link EtherChannel.
* **Access:** Every access switch maintains one uplink to each distribution switch in its office.

This topology provides multiple alternate network paths and allows routing, first-hop redundancy, EtherChannel, and spanning-tree technologies to be implemented and tested within the lab.

---

# Device Connection Overview

| Device | Role                  | Primary Connections                        |
| ------ | --------------------- | ------------------------------------------ |
| R1     | Edge Router           | ISPA, ISPB, CSW1, CSW2                     |
| CSW1   | Core Switch           | R1, CSW2, DSW-A1, DSW-A2, DSW-B1, DSW-B2   |
| CSW2   | Core Switch           | R1, CSW1, DSW-A1, DSW-A2, DSW-B1, DSW-B2   |
| DSW-A1 | Office A Distribution | CSW1, CSW2, DSW-A2, ASW-A1, ASW-A2, ASW-A3 |
| DSW-A2 | Office A Distribution | CSW1, CSW2, DSW-A1, ASW-A1, ASW-A2, ASW-A3 |
| ASW-A1 | Office A Access       | DSW-A1, DSW-A2, LWAP1, WLC1                |
| ASW-A2 | Office A Access       | DSW-A1, DSW-A2, Phone1                     |
| ASW-A3 | Office A Access       | DSW-A1, DSW-A2, Phone2                     |
| DSW-B1 | Office B Distribution | CSW1, CSW2, DSW-B2, ASW-B1, ASW-B2, ASW-B3 |
| DSW-B2 | Office B Distribution | CSW1, CSW2, DSW-B1, ASW-B1, ASW-B2, ASW-B3 |
| ASW-B1 | Office B Access       | DSW-B1, DSW-B2, LWAP2                      |
| ASW-B2 | Office B Access       | DSW-B1, DSW-B2, Phone3                     |
| ASW-B3 | Office B Access       | DSW-B1, DSW-B2, SRV1                       |

---


