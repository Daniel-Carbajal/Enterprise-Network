# Addressing Plan

This document summarizes the IPv4 addressing and VLAN segmentation used throughout the Enterprise Network Mega Lab.

## VLAN Networks

| Network             | VLAN | Subnet       | Default Gateway |
| ------------------- | ---: | ------------ | --------------- |
| Office A PCs        |   10 | 10.1.0.0/24  | 10.1.0.1        |
| Office A Phones     |   20 | 10.2.0.0/24  | 10.2.0.1        |
| Office B PCs        |   10 | 10.3.0.0/24  | 10.3.0.1        |
| Office B Phones     |   20 | 10.4.0.0/24  | 10.4.0.1        |
| Servers             |   30 | 10.5.0.0/24  | 10.5.0.1        |
| Wireless            |   40 | 10.6.0.0/24  | 10.6.0.1        |
| Office A Management |   99 | 10.0.0.0/28  | 10.0.0.1        |
| Office B Management |   99 | 10.0.0.16/28 | 10.0.0.17       |

The default gateways for user VLANs are provided through HSRP virtual IP addresses on the redundant distribution switches.

## Infrastructure Addressing

Point-to-point Layer 3 connections between the edge, core, and distribution layers use dedicated /30 IPv4 networks.

Loopback interfaces use /32 addresses for stable Layer 3 device identification and routing.

## Internet Edge

R1 connects to two simulated ISPs using the following public IPv4 networks:

| Connection | Network        |
| ---------- | -------------- |
| R1 to ISPA | 203.0.113.0/30 |
| R1 to ISPB | 203.0.113.4/30 |

NAT/PAT is performed at the edge router to provide external connectivity for internal private networks.

## Addressing Design

The addressing scheme separates user, voice, wireless, server, and management traffic while preserving a structured hierarchy for routed infrastructure links.

This segmentation supports routing, redundancy, access control, troubleshooting, and network management throughout the lab.

